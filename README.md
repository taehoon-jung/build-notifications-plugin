# 1. Latest release
> https://git.prod.sktelecom.com/advanced-deveopment/build-notifications-plugin/tags/skt_v1.5.0

<br>

# 2. Telegram BOT

### 이름 / 아이디
- Jenkins: @skt_jenkins_bot

### Token
- `385940343:AAH6SlsxjdnLvdegLKvQKyJUJh1dNA7Dj6k`

### Telegram Chat ID 가져오기
- 텔레그램의 대화방 ID를 가져오려면, 
  - 1:1의 경우 Private 메시지를 보낸다.
  - 그룹, 채널의 경우, 봇을 초대한다. `skt_jenkins_bot`
- `getUpdates` API를 호출하여, 채널 id를 얻는다. 
   - `-`로 시작하는 채널은 그룹, 채널
  - `+`로 시작하는 채널은 Private 메시지
- https://api.telegram.org/bot385940343:AAH6SlsxjdnLvdegLKvQKyJUJh1dNA7Dj6k/getUpdates

```
{
    "ok": true,
    "result": [
        {
            "update_id": 166339618,
            "message": {
                "message_id": 48,
                "from": {
                    "id": 187248447,
                    "first_name": "Taehoon",
                    "last_name": "Jung",
                    "username": "taehoonjung"
                },
                "chat": {
                    "id": -229116175,
                    "title": "Bot",
                    "type": "group",
                    "all_members_are_administrators": true
                },
                "date": 1500007751,
                "left_chat_participant": {
                    "id": 385940343,
                    "first_name": "Jenkins",
                    "username": "skt_jenkins_bot"
                },
                "left_chat_member": {
                    "id": 385940343,
                    "first_name": "Jenkins",
                    "username": "skt_jenkins_bot"
                }
            }
                ]
            }
        }
    ]
}
```

<br>

# 3. Jenkins 에 `hpi` 플러그인  등록 및 설정

- 위치
  - 환경설정 - Jenkins 관리 - 플러그인 관리 - 고급 탭 - hpi 등록
- 시스템 설정으로 이동하여, bot-token 을 등록
![스크린샷_2017-07-14_오후_1.24.04](/uploads/82400591f0d17658612d8402b998d0d6/스크린샷_2017-07-14_오후_1.24.04.png)

<br>

# 4.  Jenkins Job 설정
- 빌드 후 조치 추가 > `Telegram Notification`추가
- Global Notification에 Chat-ID를 `,`로 구분하여 추가 
- Send if success? 를 체크해야 빌드가`성공`한 경우에도 발송됨
  - 기본은 성공하지 않았을 경우에 발송
  - 고급 옵션의 Success Notification을 추가로 등록해도됨
![스크린샷_2017-07-14_오후_2.17.07](/uploads/587b9597bd1730c4058f5b5e06343b43/스크린샷_2017-07-14_오후_2.17.07.png)




# Jenkins Build Notifications Plugin

---

**This plugin is now maintained at the Jenkins GitHub Organization**

https://github.com/jenkinsci/build-notifications-plugin

---

This is a plugin to enable build notifications through [Pushover][], [Telegram][] or even [Boteco][].

## How to build

Just execute a `mvn package` and upload the *hpi* package to your Jenkins instance.

## How to configure

There are global and specific options:

### Global options

Global options should be configured in Jenkins System Configuration. You'll need to set
an Application Token for Pushover and/or a Bot Token for Telegram.

### Specific options

There are per-job configurations. You need to add a post-build step (there is a separated
step for each notification service) and configure the target to receive notifications.

## How you'll be notified

Notifications will include:

- The project's name
- The build number
- The build result
- The build's changes
- The build link

If you are receiving notifications through Pushover, the notification will be sent with
high priority in case of a fail build, low priority in case of a success build and normal
priority for the other cases.

Note that Telegram doesn't have a way to set priority for messages (and is understandable
because Telegram is a chat platform and not a notification platform like Pushover).

## How to contribute

Open an issue, spread the project, use it, fork it...

[pushover]: <http://pushover.net/>
[telegram]: <https://telegram.org/>
[boteco]: <https://github.com/devnull-tools/boteco>

# RealtimeBoard webhook Java example

This is a simple example project illustrating how to implement a [Webhooks endpoint](https://developers.realtimeboard.com/v3.0/docs/introduction-to-webhooks).

### Requirements

- Java 1.8 or later

You can check Java version by running ```java -version``` command in terminal.
If you need, you can take latest version from [here](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
### Instructions

1. Clone the repository:
```bash
git clone https://github.com/realtimeboard/webhook-java-example
```

2. [Create Your App](https://developers.realtimeboard.com/v3.0/docs/getting-started)

3. After the app is created, go to ```App Credentials``` and copy ```Webhook verification token```. Paste this verificationToken to this file: 
```
src/main/resources/application.yml
```

4. If your server is not directly visible from the internet, you can use [ngrok](https://ngrok.com/) to create a tunnel:
```bash
ngrok http 8085
```

5. Run the project:
```bash
./mvnw spring-boot:run
```
Monitor console with the results, after some runtime you should expect something like this:
```
2018-12-14 14:44:33.436  INFO 25284 --- [nio-8085-exec-1] c.r.s.controller.WebhooksController      : RealtimeBoard event accepted: RtbWebhook(type=url.verification, user=null, account=null, timestamp=0, challenge="challenge_string", comment=null, collaboration=null)
```

6. Go to application settings web-page. You need to do 3 things:
  - enable Webhooks
  - Set the scopes for your webhooks (creation of comments, invitation to board or invitation to account)
  - Set the **Webhook server url**, e.g. `https://8609bd4f.ngrok.io/webhooks`.

7. Install the app using ```Get OAuth Token``` button or [authorization section](https://developers.realtimeboard.com/v3.0/reference#authorization-and-authentication) in the docs.
Store your token somehwere safe.

8. You can then create test events on your RealtimeBoard account and view the logs of the app to check that the events were correctly received and verified.

This is an example of what you should see in your java-app console for triggered event "create comment":
```
2018-12-14 15:22:29.478  INFO 25284 --- [nio-8085-exec-8] c.r.s.controller.WebhooksController      : RealtimeBoard event accepted: RtbWebhook(type=board.comment.create, user=RtbUser(id=user_id, email=email@account.com, name=some_name), account=RtbAccount(id=account_id, name=MyTestTeam), timestamp=1544782949710, challenge=null, comment=RtbComment(id=comment_id, message=RtbMessage(id=message_id, text=Hello World! , mentions=[]), board=RtbBoard(id=board_id, name=Untitled, key=board_key=, owner=RtbUser(id=user_id, email=email@account.com, name=some_name))), collaboration=null)
```

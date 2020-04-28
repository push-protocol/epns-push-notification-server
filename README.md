# EPNS Push Notification Server
The Push Notification Server handles registration of push notification device tokens, updation and deletion of it, it also handles sending push notifications as well as listening to events of EPNS protocol to form notification payload.

- To know more about EPNS and the general specs, please jump to [EPNS General Specs](https://github.com/ethereum-push-notification-system/epns-specs/blob/master/README.md).
- To know more about EPNS Mobile App, please jump to [EPNS Mobile App](https://github.com/ethereum-push-notification-system/epns-mobile-app/blob/master/README.md)

# Technical Details
Following definitions are used in the rest of the spec to refer to a particular category or service.
| Service  | Service Resolver | Description
| ------------- | ------------- | ------------- |
| Push Registration | pushregister.epns.io | The service authenticates and registers push device tokens (not crypto token) to a wallet, it also is responsible to updating and deleting these tokens |
| Push Dispatch | pushdispatch.epns.io | This service works on the server and only accepts request coming from the server itself, it is responsible for sending push notications out and handling deleting of tokens via pushregister.epns.io |
| Push Listener | pushlisten.epns.io | This service creates a websocket to [Infura socket api](https://github.com/ethereum/go-ethereum/wiki/RPC-PUB-SUB), it listens for **App Owners** creation, updation and keeps track of messages of **App Owner Groups**, it also keeps on building a cache of users in **App Owner Groups** which the *Push Dispatch* can use to create messages. To learn more about these terminologies, head to [EPNS General Specs](https://github.com/ethereum-push-notification-system/epns-specs/blob/master/README.md) |

**Note:** Learn about [Apple Device Tokens](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns) or [Google Device Tokens](https://developers.google.com/web/ilt/pwa/introduction-to-push-notifications) used for Push Notificaiton.

### Features
The EPNS Push Notification Server is made up of three services defined above, using these, it enables the following features:
- **Push Registration Service** is used to handle authentication, registration and updation of push tokens
- **Push Dispatch Service** constructs the necessary payload and the specific users to which the payload will be delivered by talking with **Push Registration Service** and **Push Listener Service**
- **Push Listener Service** handles events that happen on the smart contract to create, cache and detect notifications, app owners, etc

### Tech Spec
Further specs and details are available inside each service. 

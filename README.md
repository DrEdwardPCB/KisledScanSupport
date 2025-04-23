<details>
<summary>
Welcome to your Expo app 👋
</summary>
This is an [Expo](https://expo.dev) project created with [`create-expo-app`](https://www.npmjs.com/package/create-expo-app).

## Get started

1. Install dependencies

    ```bash
    npm install
    ```

2. Start the app

    ```bash
     npx expo start
    ```

In the output, you'll find options to open the app in a

-   [development build](https://docs.expo.dev/develop/development-builds/introduction/)
-   [Android emulator](https://docs.expo.dev/workflow/android-studio-emulator/)
-   [iOS simulator](https://docs.expo.dev/workflow/ios-simulator/)
-   [Expo Go](https://expo.dev/go), a limited sandbox for trying out app development with Expo

You can start developing by editing the files inside the **app** directory. This project uses [file-based routing](https://docs.expo.dev/router/introduction).

## Get a fresh project

When you're ready, run:

```bash
npm run reset-project
```

This command will move the starter code to the **app-example** directory and create a blank **app** directory where you can start developing.

## Learn more

To learn more about developing your project with Expo, look at the following resources:

-   [Expo documentation](https://docs.expo.dev/): Learn fundamentals, or go into advanced topics with our [guides](https://docs.expo.dev/guides).
-   [Learn Expo tutorial](https://docs.expo.dev/tutorial/introduction/): Follow a step-by-step tutorial where you'll create a project that runs on Android, iOS, and the web.

## Join the community

Join our community of developers creating universal apps.

-   [Expo on GitHub](https://github.com/expo/expo): View our open source platform and contribute.
-   [Discord community](https://chat.expo.dev): Chat with Expo users and ask questions.
</details>

# KisledScanner

this app is developed to cater the use case of scanning + webhooks, as AI Era comes, many jobs can be done through automation. From that webhooks will be one of them.
this leads to the question that what is the best to trigger them. this app provides a solution for web hooks triggering and also have solutions to automate trigger of OCR and Data

## high level views

```
|-Camera
|-ManualInput
|-Webhooks
| |-List
| |-View
| |-Create
| |-Update
| |-History
|-Credentials
| |-List
| |-View
| |-Create
| |-Update
|- help
|-success
|-error
|-loading
```

## storage design

```mermaid
classDiagram

  class webhooks{
      id string
      name string
      method enum
      url string
      authenticationType enum
      credentialsId string
   }
   class credentials{
      id string
      name string
      type enum
      value credentials
   }
   class basicCredentials{
      username string
      password string
   }
   class jwtCredentials{
      jwtType enum
      publicKey string
      privateKey string
      passphrase string
      algorithm enum
      payload object
   }
  class headerCredentials{
      key string
      value string
   }
   class camera{
      webhookid string
   }
   class photo{
      webhookid string
   }
   class manualinput{
      webhookid string
   }
   class code{
      webhookid string
   }
   class history{
      webhookId string
      calledAt date
      trigger enum
      status enum
   }

```

### Code flow

```mermaid
   flowchart
      idle[Camera page]---->camera
      camera["Camera sees QRCode"]
      selectedWebHooks["code webhooks"]
      hasSelectedWebhooks{has webhooks}
      sendRequest{send request}
      prompt{"prompt for send"}
      camera & selectedWebHooks ---->hasSelectedWebhooks
      hasSelectedWebhooks--yes-->prompt
      prompt--approve-->sendRequest
      sendRequest--success-->showSuccessPage---->idle
      sendRequest--error-->showErrorPage---->idle
      prompt--cancel-->idle
      hasSelectedWebhooks--"no"-->warn---->idle

```

### Camera flow

```mermaid
   flowchart
      idle[Camera page]---->camera
      camera["user capture"]
      selectedWebHooks["camera webhooks"]
      hasSelectedWebhooks{has webhooks}
      sendRequest{send request}
      prompt{"prompt for send"}
      camera & selectedWebHooks ---->hasSelectedWebhooks
      hasSelectedWebhooks--yes-->prompt
      prompt--approve-->sendRequest
      sendRequest--success-->showSuccessPage---->idle
      sendRequest--error-->showErrorPage---->idle
      prompt--cancel-->idle
      hasSelectedWebhooks--"no"-->warn---->idle

```

### Manual input flow

```mermaid
   flowchart
      idle[Manual input page]---->field
      field["user input"]
      selectedWebHooks["manualinput webhooks"]
      hasSelectedWebhooks{has webhooks}
      sendRequest{send request}
      prompt{"prompt for send"}
      field & selectedWebHooks ---->hasSelectedWebhooks
      hasSelectedWebhooks--yes-->prompt
      prompt--approve-->sendRequest
      sendRequest--success-->showSuccessPage---->idle
      sendRequest--error-->showErrorPage---->idle
      prompt--cancel-->idle
      hasSelectedWebhooks--"no"-->warn---->idle

```

### Manual input flow

```mermaid
   flowchart
      idle[Manual input page]---->field
      field["user input"]
      selectedWebHooks["manualinput webhooks"]
      hasSelectedWebhooks{has webhooks}
      sendRequest{send request}
      prompt{"prompt for send"}
      field & selectedWebHooks ---->hasSelectedWebhooks
      hasSelectedWebhooks--yes-->prompt
      prompt--approve-->sendRequest
      sendRequest--success-->showSuccessPage---->idle
      sendRequest--error-->showErrorPage---->idle
      prompt--cancel-->idle
      hasSelectedWebhooks--"no"-->warn---->idle

```

# 🚀 Quick Start with Compose Entity (CE framework)

*July 11, 2025 — Android Studio, Compose Entity, Compose Entity KSP*

Everything looks simple, but each app must have a **unique package name**.  
So you’ll need to replace a few things — but it won’t take more than **10 minutes**.  
In return, CE gives you tools that save **up to 90%** of the time from idea to working prototype.

---

### 🧩 Steps to Start

1. **Download the latest release archive**  
   → [https://github.com/SergeyBoboshko/ComposeEntitySample/releases/](https://github.com/SergeyBoboshko/ComposeEntitySample/releases/)

2. **Unzip the archive**  
   Extract it into a convenient folder, for example:  
   `D:\work\Android\CE Template\ComposeEntitySample-2\`

3. **Create a new Jetpack Compose project**  
   In Android Studio, create a new project with an **Empty Compose Activity**.

4. **Copy source files from the release package**  
   The release always uses this package:  
   `io.github.sergeyboboshko.cereport`  
   Suppose your new project uses:  
   `com.example.myapp333`

   Then copy **all files with replacement** from: `d:\work\Android\CE Template\ComposeEntitySample-2\app\src\main\java\io\github\sergeyboboshko\cereport\` into `YourProject\app\src\main\java\com\example\myapp333\`

5. **Copy `app`-level Gradle files**  
Go to the `app` folder of both the release and your project.  
Copy the following files from the release to your project (overwrite if asked):
- `build.gradle.kts`
- `proguard-rules.pro` *(optional)*

6. **Copy root-level Gradle files**  
Go up one level to the project root in both the release and your project.  
Copy and overwrite these files:
- `build.gradle.kts`
- `settings.gradle.kts`

---

### 🛠️ Final Adjustments Before Launch

7. **Fix the package name throughout the project**

After switching back to Android Studio, you will likely see **many errors** in your new project.  
That’s normal — let’s fix the package name globally:

- Open the file `MainActivity.kt`
- Copy the current package name (it will be: `io.github.sergeyboboshko.cereport`)
- Now do a **global replace** in Android Studio:

  **Steps:**
  1. In the Project view (left panel), right-click the root node:
     - In *Android view*, right-click `app`
     - In *Project view*, right-click the project name
  2. Choose **"Replace in Files..."**
  3. In the "Find" field, paste:  
     `io.github.sergeyboboshko.cereport`
  4. In the "Replace with" field, enter your package:  
     `com.example.myapp333`
  5. Click **"Replace All"**

---

8. **Update app name in `strings.xml`**

Open the file: `app/src/main/res/values/strings.xml`
Find this line:
```xml
<string name="app_name">Compose Entity Sample</string>
```

Replace "Compose Entity Sample" with your app’s actual name.

9. **Verify build.gradle.kts (module-level)**

Open app/build.gradle.kts. Replace this line: `rootProject.name = "Compose Entity Sample"` With your preferred project name: `rootProject.name = "MyAppName"` 

10. **Edit settings.gradle.kts**

Open: `settings.gradle.kts`
Replace this line:

```kotlin
rootProject.name = "Compose Entity Sample"
```
With your preferred project name:

```kotlin
rootProject.name = "MyAppName"
```

11. **Sync and Run**

Click “Sync Now” in the top-right corner of Android Studio.

Once Gradle finishes syncing, you can run the app.

You should see a welcome screen with a few navigation buttons.

⚠️ Important:
Do not click the Add or Edit buttons yet — they are not connected and will crash the app.

To hide these buttons temporarily, open:

`
screens/MainPage.kt
`
Inside the MainPage() function, add the following line:

```kotlin
GlobalState.hideAllBottomBarButtons()
```
This is your first customization.

Later, when you add new Entity tables, CE will automatically show the correct buttons for CRUD operations.

🖼️ What You’ll See After Launch
Below are screenshots comparing the released sample and your new project layout.

<img width="461" height="1024" alt="image" src="https://github.com/user-attachments/assets/26def920-8cda-4146-bc66-5199257aa838" />

<img width="1024" height="729" alt="image" src="https://github.com/user-attachments/assets/2ea078c2-d25c-4b07-9e21-c50ee1679d5c" />




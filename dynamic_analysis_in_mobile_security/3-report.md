Challenge 3: Android Security Challenge – Revealing Hidden Functions

Objective

Analyze and reverse engineer an Android application to find and invoke hidden functions that are never triggered in the standard UI flow. These functions contain logic to retrieve and decrypt a hidden flag.

Tools Used

Frida

Objection

GDB

APKTool

JADX

Android Emulator

Python (for decoding logic)

Step-by-Step Process

1. Decompiling and Inspecting APK

Decompiled Apk_task3 using jadx.

Located class HiddenFlagUtil containing:

A method that returned a hex-encoded string.

Another function that appeared to process that string but was never invoked in the normal UI flow.

2. Identifying Hidden Methods

Used Objection to list all classes and methods:

objection -g com.example.apk_task3 explore
android hooking list classes | grep Hidden
android hooking list class_methods com.example.HiddenFlagUtil

Identified:

private String getEncryptedFlag()

private String decryptFlag(String input)

3. Invoking Hidden Functions Dynamically

Hooked the class and invoked methods using Frida:

Java.perform(function () {
  var HiddenUtil = Java.use("com.example.HiddenFlagUtil");
  var encrypted = HiddenUtil.getEncryptedFlag();
  var decrypted = HiddenUtil.decryptFlag(encrypted);
  console.log("Decrypted Flag: " + decrypted);
});

Successfully retrieved:

Decrypted Flag: FLAG{hidden_function_hacked}

4. Manual Function Testing (Alternative via Objection)

Loaded app with Objection:

android hooking invoke_method com.example.HiddenFlagUtil getEncryptedFlag
android hooking invoke_method com.example.HiddenFlagUtil decryptFlag "<encrypted_value>"

Output confirmed the decrypted flag.

Challenges Faced

Methods were not exposed in the main activity.

GDB was explored initially but Frida proved simpler for this case.

Frida required exact class/method signatures which had been obfuscated slightly.

Result

Decrypted Flag:FLAG{hidden_function_hacked}


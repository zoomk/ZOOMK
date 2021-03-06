<?xml version="1.0" encoding="UTF-8"?>

<plugin xmlns="http://apache.org/cordova/ns/plugins/1.0"
	xmlns:android="http://schemas.android.com/apk/res/android"
	id="cordova-plugin-qq"
	version="0.9.8">
	
    <name>QQ</name>
	<description>Cordova plugin for Tencent QQ Open SDK</description>
	<author>Liming Xie</author>
	<license>MIT</license>
	<keywords>rjfun,admob,google,ad</keywords>
    <repo>https://github.com/floatinghotpot/cordova-plugin-qq.git</repo>
    <issue>https://github.com/floatinghotpot/cordova-plugin-qq/issues</issue>

	<engines>
	    <engine name="cordova" version=">=3.0" />
	</engines>

    <js-module src="www/QQ.js" name="QQ">
        <clobbers target="window.QQ" />
    </js-module>

	<dependency id="cordova-plugin-extension" />
	
    <!-- android -->
    <platform name="android">
        <config-file target="AndroidManifest.xml" parent="/manifest/application">
            <activity
            android:name="com.tencent.tauth.AuthActivity" 
            android:noHistory="true" 
            android:launchMode="singleTask" >
                <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="tencent1104702980" />
                </intent-filter>
            </activity>
            
            <activity android:name="com.tencent.connect.common.AssistActivity"
                android:theme="@android:style/Theme.Translucent.NoTitleBar"
                android:configChanges="orientation|keyboardHidden|screenSize" 
                />
        </config-file>
        
        <config-file target="AndroidManifest.xml" parent="/*">
			<uses-permission android:name="android.permission.INTERNET"/>
			<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
			<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        </config-file>
          
        <config-file target="res/xml/config.xml" parent="/*">
            <feature name="QQ">
                <param name="android-package" value="com.rjfun.cordova.qq.QQPlugin"/>
                <param name="onload" value="true" />
            </feature>
        </config-file>
        
        <source-file src="src/android/QQPlugin.java" target-dir="src/com/rjfun/cordova/qq" />

        <source-file src="src/android/mta-sdk-1.6.2.jar" target-dir="libs" />
        <source-file src="src/android/open_sdk_r5043.jar" target-dir="libs" />
        
        <framework src="com.android.support:support-v4:+" />

     </platform>
     
     <!-- ios -->
     <platform name="ios">
         <config-file target="config.xml" parent="/*">
             <feature name="QQ">
                 <param name="ios-package" value="QQPlugin" />
                 <param name="onload" value="true" />
             </feature>
         </config-file>

         <config-file target="*-Info.plist" parent="CFBundleURLTypes">
            <array>
                <dict>
                    <key>CFBundleTypeRole</key>
                    <string>Editor</string>
                    <key>CFBundleURLName</key>
                    <string>tentcentopenapi</string>
                    <key>CFBundleURLSchemes</key>
                    <array>
                        <string>tencent1104702980</string>
                    </array>
                </dict>
            </array>
         </config-file>

         <header-file src="src/ios/QQPlugin.h"/>
         <source-file src="src/ios/QQPlugin.m"/>
         
         <framework src="src/ios/TencentOpenAPI.framework" custom="true" />
         <resource-file src="src/ios/TencentOpenApi_IOS_Bundle.bundle"/>

         <framework src="CoreGraphics.framework" />
         <framework src="CoreTelephony.framework" />
         <framework src="SystemConfiguration.framework" />
         <framework src="Security.framework" />
         <framework src="libiconv.dylib" />
         <framework src="libsqlite3.dylib" />
         <framework src="libstdc++.dylib" />
         <framework src="libz.dylib" />
	</platform>

</plugin>

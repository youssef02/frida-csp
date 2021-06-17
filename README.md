# frida-csp

this is more of what i learned on the journey and wanted to share

the objectif is to reverse engineer an android app : clipstudiopaint apk and making it work 
this is more of a challenge than causing problem as i keep learning:
so what is the start point :

    ClipStudio apk is a native app(meaning it was built using ndk) using C++ from what i saw on cutter

    0x634eec0 > VEFormLoginView::PushLoginButton that the login function on the app it got triggered when you want to connect to your account

i found out that there is some stuff you need to do it,i tryed to find what else in the libClipStudioPaint.so file 

saldy you cant hook to that 0x634eec0 as it is a form event meaning while using frida it does not give us a return value or args that we can use

i noticed also that clipstudio track your location on login from cameralocation something

    0x01d0cf70 > method.Odyssey::ODCCameraLocation.GetLatiLongiTwist_unsigned_int__const
    
    when i searched for strings i found that there is some stuff to consider like:
    
    
        response.xml you get from login i gess?
        sql collumn names including one related to account as it is. storred 
        also they have some of expandingbonus login 
        

manyways to hack the app, i gess the best approach is like the following:


on login bypass the check and call function to create the user with fake data, disactivate the check function change somefunction from login or sqlite to add expiration to 2999, 

Update #2 

What do you think if isexpired returned false on every Call.

Will try to compile as it take time to patch and assemble the APK. if this work, i am taking a huge vacation 

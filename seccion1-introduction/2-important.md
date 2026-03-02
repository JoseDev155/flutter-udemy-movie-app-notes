# 2. Important

Hi,

As many of you might or might not know Dart out of the box now supports sound null-safety. If you are using Flutter version 2.x then most probably the source code demonstrated in the videos will not work as intended. The course was recorded before the release of Flutter 2 and hence the code displayed does not account for null-safety.



However, the project source files available on Github have now been upgraded to account for null-safety and are Flutter 2.x compatible. Hence, I'd recommend that before you start the course that you upgrade your Flutter SDK to 2.0 or higher. Use the command below to upgrade flutter.

```bash
flutter upgrade
```

If at any point you encounter an error regarding null-safety refer the Github source code.



The changes to the source code were so minuscule that it did not warrant me to rerecord all the lectures. It is quite a tedious task to record and edit these videos. I hope you'll understand.



NOTE: Please update the pubspec.yaml dependencies section to reflect the dependencies section of the pubspec.yaml file provided in the github source code. You will need to upgrade the different packages we use in the project to versions that account for null-safety for the application to compile properly.



Thanks,

Hussain Mustafa

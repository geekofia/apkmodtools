#### Disclaimer
This is just a collection of tools i use personally. I hereby declare that the tools available in this repo are not developed by me. The original author of these tools have the complete rights.

**[apktool](https://ibotpeaches.github.io/Apktool/) | [signapk](https://source.android.com/devices/tech/ota/sign_builds.html)**

#### Steps To Build MOD App
SL No. | Steps | Tools
-------|-------|------
1 | Decompile | apktool
2 | Edit | any text editor
3 | Recompile | apktool
4 | Sign | signapk

#### Installation

1. Download zip from [releases](https://github.com/geekofia/apkmodtools/releases) and extract to where you want to save (i.e $HOME).
1. Add your extracted directory to `PATH` & reload `~/.bashrc`:

    ```
    echo 'export PATH="<your_extracted_directory_path>:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    ```

    example:

    ```
    $ echo 'export PATH="$HOME/apkmodtools:$PATH"' >> ~/.bashrc
    $ source ~/.bashrc
    ```
1. check installation:

    ```
    which apktool
    which signapk
    ```

    example:

    ```
    $ which signapk
    /home/chankruze/apkmodtools/signapk
    $ which apktool 
    /home/chankruze/apkmodtools/apktool
    ```
1. create `apktool/framework` folder to supress couldn't write to warning by apktool:

   (`WARNING: Could not write to (/home/chankruze/.local/share/apktool/framework), using /tmp instead...`)
    ```
    mkdir -p ~/.local/share/apktool/framework
    ```

#### Usage

1. **Apktool usage:** https://ibotpeaches.github.io/Apktool/documentation/
1. **Signing Apk:**
    I have created a wrapper script to ease the process. By default the wrapper script usage certificate (`certificate.pem`) & key (`key.pk8`) found in this zip. If you wan to use your own, then replace these 2 files (name should be same as the existing) in your installation directory.

    Note:
    - `certificate.pem` is in format `publickey.x509[.pem]`
    - `key.pk8` is in format `privatekey.pk8`

    To sign newly compiled apk execute below command:

    ```
    signapk <compiled_apk.apk> <name_to_save.apk>
    ```

#### Complete Example:

```
chankruze@geekofia:~/Lab$ ls
YTMusic.apk

chankruze@geekofia:~/Lab$ apktool d YTMusic.apk 
I: Using Apktool 2.4.0 on YTMusic.apk
I: Loading resource table...
I: Decoding AndroidManifest.xml with resources...
I: Loading resource table from file: /home/chankruze/.local/share/apktool/framework/1.apk
I: Regular manifest package...
I: Decoding file-resources...
I: Decoding values */* XMLs...
I: Baksmaling classes.dex...
I: Baksmaling classes2.dex...
I: Copying assets and libs...
I: Copying unknown files...
I: Copying original files...

chankruze@geekofia:~/Lab$ apktool b -o YT-New.apk YTMusic
I: Using Apktool 2.4.0
I: Checking whether sources has changed...
I: Smaling smali folder into classes.dex...
I: Checking whether sources has changed...
I: Smaling smali_classes2 folder into classes2.dex...
I: Checking whether resources has changed...
I: Building resources...
I: Copying libs... (/lib)
I: Building apk file...
I: Copying unknown files/dir...
I: Built apk...

chankruze@geekofia:~/Lab$ ls
YTMusic  YTMusic.apk  YT-New.apk

chankruze@geekofia:~/Lab$ signapk YT-New.apk YT-New-signed.apk 

chankruze@geekofia:~/Lab$ ls
YTMusic  YTMusic.apk  YT-New.apk  YT-New-signed.apk
```
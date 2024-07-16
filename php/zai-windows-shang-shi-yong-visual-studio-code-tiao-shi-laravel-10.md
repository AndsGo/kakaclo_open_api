# 在 Windows 上使用 Visual Studio Code 调试 Laravel 10

原文：[https://medium.com/@jtillwick/debugging-laravel-10-with-visual-studio-code-on-windows-df99d9e0a958](https://medium.com/@jtillwick/debugging-laravel-10-with-visual-studio-code-on-windows-df99d9e0a958)

## **Install VS Code** <a href="#id-060a" id="id-060a"></a>

Download the latest Visual Studio Code for Windows from [https://code.visualstudio.com/download](https://code.visualstudio.com/download).

## **Install PHP** <a href="#id-62ab" id="id-62ab"></a>

Download the latest version of PHP (8.2.10 at this time) VS16 x64 Thread Safe in Zip format from [https://windows.php.net/download](https://windows.php.net/download).

Once downloaded, unzip and rename the folder to`php`. Then move it to `C:\Program Files\php`.

## **Install Composer** <a href="#id-0dfe" id="id-0dfe"></a>

Download the Composer installer for Windows from [https://getcomposer.org/Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe).

Once run, select `Install for all users`, then select next. Leave `Developer mode` unchecked and select next. It should automatically find the`php.exe`at `C:\Program Files\php\php.exe`, if not, enter that location in the path, then check the box to `Add this PHP to your path?` and select next.

Continue through the rest of the install without changing the default options until finished.

## **Install Xdebug PHP Extension** <a href="#abdb" id="abdb"></a>

Download the Xdebug extension that corresponds to your version of PHP from [https://xdebug.org/download](https://xdebug.org/download). In this case it would be `PHP 8.2 VS16 TS (64 bit).`

It will download a`.dll` file. Rename it to `php_xdebug.dll` and place it into the path `C:\Program Files\php\ext\php_xdebug.dll`.

## **Configure PHP php.ini** <a href="#id-7f19" id="id-7f19"></a>

First, find the extensions section of the`php.ini`file by searching for `extension=` and ensure the following are uncommented:

```
extension=curl
extension=fileinfo
extension=mbstring
extension=openssl
extension=pdo_mysql
```

Next, scroll to the bottom of the file and add the following:

```
[xdebug]
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.discover_client_host=yes
xdebug.client_port=9001
xdebug.remote_port=9001
xdebug.idekey = VSCODE
xdebug.log_level=0
xdebug.remote_enable=1
xdebug.remote_autostart=1
xdebug.client_host="127.0.0.1"
zend_extension=xdebug
```

## **Install VS Code Extensions** <a href="#id-1b02" id="id-1b02"></a>

Launch VS Code and select the Extensions panel on the left sidebar or from the View menu. Enter `PHP Debug`into the search bar and install the extension.

Once installed, right click it in the sidebar and select `Extension Settings`.

For`PHP > Debug: Executable Path`click the link to open the`settings.json` file and add the following line:

```
{
  ...
  "php.debug.executablePath": "C:/Program Files/php/php.exe"
}
```

In the next section, `PHP > Debug: Ide Key` enter `VSCODE`.

## **Create VS Code launch.json** <a href="#b6cb" id="b6cb"></a>

Open the `Run and Debug`sidebar panel and click on the cog wheel icon at the top right of the panel. Select the option for `PHP (Xdebug)`. It should automatically create a `launch.json` file. Make yours look like below.

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9001,
            "env": {
                "XDEBUG_CONFIG": "log_level=7",
            }
        }
    ]
}
```

## **Debug Your Laravel Application** <a href="#b678" id="b678"></a>

Run your Laravel app from the VS Code Terminal on the bottom panel (CTRL + J) by entering the following:

```
php artisan serve
```

Once that has started successfully, go to the VS Code `Run and Debug` panel and select `Listen for Xdebug` from the drop down and press the green play button. Now anytime there is an exception thrown, or you enter a breakpoint in your code, VS Code will break on that line of code and allow you to inspect variables and step through code execution.

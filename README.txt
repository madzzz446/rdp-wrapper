Скорее всего поможет следующий  способ:

1. Запустить autoupdate.bat

2. Запустить RDPConf, убедиться, что в окне написано Running, Listening, Fully Supported.

Если не помогло:

1. Запустить cmd от имени администратора, выполнить команду

sc query TermService

2. Убедиться, что вывод команды равен

        Тип                : 30  WIN32
        Состояние          : 4  RUNNING
                                (STOPPABLE, NOT_PAUSABLE, ACCEPTS_SHUTDOWN)
        Код_выхода_Win32   : 0  (0x0)
        Код_выхода_службы  : 0  (0x0)
        Контрольная_точка  : 0x0
        Ожидание           : 0x0

т.е. состояние 4 RUNNING и Коды выхода (== ошибки) равны 0

3. Запустить RDPConf, убедиться, что в окне написано Running, Listening, Fully Supported.

4. Если вместо Fully Supported выведено красным Not Supported - скопировать файл rdpwrap.ini из данной папки в C:\Program Files\RDP Wrapper (в диалоговом окне выбрать заменить). После этого запустить RDPConf и убедиться, что Fully Supported и все остальное тоже зеленое

5. Если Not Running / Not Listening (красным текстом) - запустить uninstall.bat, затем install.bat, вернуться к шагу 3.

6. Для проверки подключений можно запустить RDPCheck и подключиться к компу (с этого компа к этому же компу)

7. Если не помогло - запускай cmd от имени администратора, выполняй 

reg add HKLM\SYSTEM\CurrentControlSet\Services\TermService\Parameters /v ServiceDll /t REG_EXPAND_SZ /d "%SystemRoot%\system32\termsrv.dll" /f

*. Полезности:

Гайд на установку + автообновление RDP Wrapper:

https://github.com/asmtron/rdpwrap/blob/master/binary-download.md

Перезапуск сервиса удаленного рабочего стола:

net stop termservice
net start termservice

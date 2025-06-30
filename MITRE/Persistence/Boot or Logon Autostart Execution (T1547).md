# Boot or Logon Autostart Execution

Злоумышленники могут настроить систему на автоматический запуск ПО при включении компьютера или входа пользователя для получения закрепления или повышения привилегий. Такой механизм существует в ОС, например существуют специальные директории, или репозитории, которые хранят конфигурационную информацию, например реестр Windows. Или модифицировать функционал ядра (Linux).

Если на старте программы работают с повышенными привилегиями, то у злоумышленника есть возможность повышения привилегий.

## Примеры

* BoxCaon обеспечил закрепление, настроив раздел реестра `HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows\load` так, чтобы он указывал на свой исполняемый файл.
  
* Mis-Type создал разделы реестра для сохранения, включая `HKCU\Software\bkfouerioyou`, `HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\{6afa8072-b2b1-31a8-b5c1-{Уникальный идентификатор}` и `HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components\{3BF41072-B2B1-31A8-B5C1-{Уникальный идентификатор}`.

## T1547.001 Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder


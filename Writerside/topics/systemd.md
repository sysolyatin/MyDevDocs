# Ubuntu Services

Необходимо создать файл

```
/etc/systemd/system/name.service
```

со следующим содержимым

```
[Unit]
Description=описание

[Service]
Type=simple
WorkingDirectory=/dir
ExecStart=/dir/binfile
ExecStop=/bin/kill -15 $MAINPID
Restart=on-failure

[Install]
WantedBy=multi-user.target
Alias=name.service
```

Команды для дальнейшего управления

```bash
sudo systemctl daemon-reload
sudo systemctl start name
sudo systemctl stop name
sudo systemctl restart name
sudo systemctl status name
sudo systemctl enable name
sudo journalctl -u name
```
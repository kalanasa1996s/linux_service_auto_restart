# Linux_service_auto_restart
Linux Service Auto Down and 15 second Auto Restart
autorestart.py




      import subprocess
      import systemd
      import time

      SERVICE_NAME = 'postgresql@12-main.service'

      def restart_service():
          subprocess.run(["systemctl", "restart", SERVICE_NAME])

      while True:
          # Check if the service is running
          status = subprocess.run(['systemctl', 'is-active', SERVICE_NAME], capture_output=True, text=True)

          if status.stdout.strip() != 'active':
              # Restart the service
              restart_service()

          # Wait for 5 seconds before checking again
          time.sleep(30)
          
          
          
# Create Service autorestart.py 
sudo nano /etc/systemd/system/test.service

    [Unit]
    Description=My test service
    After=multi-user.target
    [Service]
    Type=simple
    Restart=always
    ExecStart=/usr/bin/python3 /home/<username>/test.py
    [Install]
    WantedBy=multi-user.target
    
    
    
    sudo systemctl daemon-reload
    
    sudo systemctl enable test.service
    
    sudo systemctl start test.service

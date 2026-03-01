# VCC-Assignment2-AutoScaling
# EC2 user-data bootstrapping script for Nginx used in AWS Auto Scaling Group (VCC Assignment 2 – IIT Jodhpur).
#!/bin/bash
set -xe
if command -v dnf >/dev/null 2>&1; then
  dnf install -y nginx
else
  yum install -y nginx
fi
systemctl enable nginx
systemctl start nginx

HOST=$(hostname)
RAND=$RANDOM

cat <<EOF > /usr/share/nginx/html/index.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>VCC Assignment 2 – Auto Scaling Demo</title>
<style>
body {
  background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
  font-family: Arial;
  color: white;
  text-align: center;
  padding-top: 90px;
}
.card {
  background: rgba(0,0,0,0.4);
  width: 60%;
  margin: auto;
  padding: 40px;
  border-radius: 12px;
}
h1 { color: #00e6e6; }
.info { font-size: 20px; margin-top: 20px; }
footer { margin-top: 40px; font-size: 14px; color: #ddd; }
</style>
</head>
<body>

<div class="card">
  <h1>Auto Scaling & Load Balancing ACTIVE</h1>

  <div class="info">
    <p><b>Served By Host:</b> $HOST</p>
    <p><b>Request Token:</b> $RAND</p>
  </div>

  <footer>
    <p>VCC Assignment 2 – IIT Jodhpur</p>
    <p>Roll Number: G25AI1055</p>
  </footer>
</div>

</body>
</html>
EOF

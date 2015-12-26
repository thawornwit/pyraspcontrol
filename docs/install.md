# Install PyRaspControl

To get PyRaspControl install onto your Raspberry Pi should be fairly straight forward. The following are steps on what you need to install and manually configure to get PyRaspControl up and running.

1. Clone the project repository from GitHub:

  ```
  sudo git clone https://github.com/davidvuong/pyraspcontrol.git /var/www/pyraspcontrol
  cd /var/www/pyraspcontrol
  ```

1. Install the project (Python) dependencies:

  ```
  sudo pip install -r requirements.txt
  ```

1. Install and setup the Apache web server:

  ```
  sudo apt-get install apache2 libapache2-mod-wsgi
  ```

1. Link the PyRaspControl Apache configuration files:

  ```
  sudo cp /var/www/pyraspcontrol/pyraspcontrol.conf /etc/apache2/sites-available/pyraspcontrol.conf
  sudo ln -s /etc/apache2/sites-available/pyraspcontrol.conf /etc/apache2/sites-enabled/pyraspcontrol.conf
  ```

1. Port forward your router to map TCP connections on port 80 (external) to 8080 (internal).

  This step will depend on what router you have available. I have a billion router and after a quick Google search, I found [this site](http://portforward.com/english/routers/port_forwarding/routerindex.htm). They have router specific guides on how to port forward. I found it very useful.

  Note that if port 8080 is already being used, you can change the port PyRaspControl runs on by editing the `/pyraspcontrol/pyraspcontrol.py` file:

  ```python
  if __name__ == '__main__':
      app.run(port=<your port>)
  ```

1. Finally, restart Apache to see your changes take affect:

  ```
  sudo service apache2 restart
  ```
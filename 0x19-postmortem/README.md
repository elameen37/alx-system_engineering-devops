# Postmortem

During the release of Alx System Engineering & DevOps project 0x19 at approximately 06:07 Greenwich Mean Time (GMT), an outage occurred on an isolated Ubuntu 14.04 container running an Apache web server. When making GET requests to the server, instead of receiving the expected response of an HTML file defining a simple Holberton WordPress site, a 500 Internal Server Error was encountered.

## Debugging Process

LMN INFOHUB identified the issue when starting the project at around 19:20 GMT. The following steps were taken to address the problem:

1. Checked the running processes using the command ps aux. Confirmed that two apache2 processes, namely root and www-data, were running correctly.

2. Explored the /etc/apache2/sites-available folder to determine that the web server was serving content from /var/www/html/.

3. Executed strace on the PID of the root Apache process in one terminal while making a curl request to the server in another terminal. However, no useful information was obtained from the strace command.

4. Repeated the previous step, but this time using the PID of the www-data process. Encouragingly, the strace output revealed an -1 ENOENT (No such file or directory) error when attempting to access the file /var/www/html/wp-includes/class-wp-locale.phpp.

5. Conducted a manual search through the files in the /var/www/html/ directory, utilizing Vim pattern matching to locate the erroneous .phpp file extension. Discovered it in the wp-settings.php file on line 137 (require_once( ABSPATH . WPINC . '/class-wp-locale.php' );).

6. Rectified the issue by removing the trailing p from the line.

7. Tested another curl request on the server, which returned a successful 200 status.

8. Created a Puppet manifest to automate the fix for this error.


## Summary

In summary, the issue was attributed to a typographical error. Specifically, the WordPress application encountered a critical error in wp-settings.php when trying to load the file class-wp-locale.phpp. The correct file name, which should have been located in the wp-content directory of the application folder, is class-wp-locale.php.

The patch involved a simple correction of the typo by removing the trailing `p`.

## Prevention

This outage was not caused by a web server error but rather an application error. To prevent similar outages in the future, consider the following measures:

* Thorough testing before deploying the application. This error could have been identified and addressed earlier through comprehensive testing.

* Implementing status monitoring by enabling an uptime monitoring service such as UptimeRobot [UptimeRobot](./https://uptimerobot.com/). This would provide instant alerts in the event of a website outage.

Additionally, in response to this error, a Puppet manifest was written, which can be found at [0-strace_is_your_friend.pp](https://github.com/elameen37/alx-system_engineering-devops/blob/master/0x17-web_stack_debugging_3/0-strace_is_your_friend.pp)

The manifest automates the fix for any similar errors by replacing phpp extensions with php in the 
/var/www/html/wp-settings.php file.

However, it is worth noting that such errors are unlikely to occur again because, as programmers, we never make mistakes! :wink:
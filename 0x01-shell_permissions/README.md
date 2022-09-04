0 - su - switches current user to another user <br><br>
1 - whoami - prints the effective username of the current file <br><br>
2 - groups - prints all the groups that current user is part of <br><br>
3 - chown  - changes the owner of a file to another file user <br><br>
4 - touch  - creates an empty file <br><br>
5 - chmod u+x - adds execute permission to the owner of a file <br><br>
6 - chmod ug+x,o+r - adds execute permission to the owner and the group owner, and read permission to the other users and to the file <br><br>
7 - chmod a+x - adds execute permission to the owner, the group owner, and to the other users, to the file <br><br>
8 - chmod 007 - sets the permission to a file as follows. owner:no permission, group: no permission, other users:all permission<br><br
>
9 - chmod 753 - sets mode of file to this  <br><br>
10 - chmod --reference=olleh hello - sets the mode of the file hello thesame as olleh's mode <br><br>
11 - chmod a+X * - adds execute permission to all subdirectories of the current directory for the owner, group owner and all other users. Regular files should not be changed.<br><br>
12 - mkdir -m 751 my_dir - creates a directory called my_dir with permission 751 in the working directory.<br><br>
13 - chgrp school hello  - changes the group owner to school for the file hello <br><br>

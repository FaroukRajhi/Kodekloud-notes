# Create a system account called apachedev

sudo useradd --system apachedev

# Jane's account i.e jane is expired.Unexpire the same and make sure it never expires again.

usermod jane -e "" 

# Mark the password for jane as expired to force her to immediately change it the next time she logs in.

sudo chage --lastday 0 jane

# Make sure the user jane gets a warning at least 2 days before the password expires.

# Edit the PAM configuration file for the su utility so that this utility only accepts the requests from users that are part of the wheel group.

sudo vi /etc/pam.d/su

Uncomment below given line:


#auth           required        pam_wheel.so use_uid



so, it should look like


auth           required        pam_wheel.so use_uid

# Edit again the PAM configuration file for the su utility so that the requests from the users that are the member of the wheel group should be accepted immediately, without asking for any password.

Uncomment below given line:


#auth           sufficient      pam_wheel.so trust use_uid



so, it should look like


auth           sufficient      pam_wheel.so trust use_uid

# Restrict the root access to SSH service via PAM

You can use the pam_listfile.so module which offers great flexibility in limiting the privileges of specific accounts. Please make sure you don't restrict the root SSH access from the SSH configuration.

sudo vi /etc/pam.d/sshd

Add below given line at the end of the file and save it:


auth    required       pam_listfile.so onerr=succeed  item=user  sense=deny  file=/etc/ssh/deniedusers



Now create /etc/ssh/deniedusers file


sudo vi /etc/ssh/deniedusers



Add root user in the file, so its content should look like this:


root

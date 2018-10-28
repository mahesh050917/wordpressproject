# wordpressproject
Setup a DevOps pipeline for Wordpress
Below is the steps on what the script does when triggered:

  1)  Check which repository branch the build (origin/staging or origin/master) is triggered.
  2)  If this is the first build, create database and restore the db.sql which is also included in the repository for initial deployment. Also creates the user, password and assign the correct permission to the db.
  3)  Additionally, if the build comes from the master branch, we run a different script that creates a cpanel account for the wordpress instance.
  4)  I have a base Wordpress files located in the root folder which I rsync to the project webroot then issue another rsync this time from the target jenkins workspace which looks like /var/lib/jenkins/workspace/[JOBNAME]
  5)  At this point, we have all the required and updated files from the repo to make the website work except for the wp-config.php file in which the scripts creates by copying the content wp-config-sample file in the base Wordpress directory. It then replace all placeholders (e.g $DB_HOST, $DB_USER, $DB_PASSWORD) with real data we generated in the script

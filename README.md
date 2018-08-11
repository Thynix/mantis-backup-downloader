### Cronjob-capable shell script to download backups from Mantis bugtracker

This script:
- automatically logs in to Mantis, see section "Configuration" in the
  script.
- tells Mantis to create a fresh backup.
- checks whether the date of the backup as reported by Mantis matches
  the local time to ensure backup creation worked.
- downloads the backup into a directory called YYYY-MM-DD, or fails
  if it already exists.
- tests the CRCs of the zip files of the backup.
- sets the timestamps of the zip files to that of the newest contained
  file.
- aborts with non-zero exit code and prints an error if any of the above
  fails. If your have a working ```mail``` command available on your
  system cron daemons such as ```anachron``` will typically mail this
  output to you.
- prints nothing upon success to ensure you don't get unnecessary emails
  from cron.

**Notice**: As of 2018 it seems the feature to create a backup on the
web interface is only available on MantisHub, not in stock Mantis.
Hence this script likely only will work with MantisHub.

### Script for encrypting the backups

As a bonus feature the script `encrypt-mantis-backup` can be used to:
- encrypt the backup of the current day to a recipient's GPG key and
  create a signature file (make sure the user which runs it has a GPG
  private key which is not password protected!).
- automatically download the recipient's GPG key at every run to check
  for revocation.
- place the encrypted and signed backup in a different directory, and
  set the permissions of the directory / files as specified.
  This e.g. allows putting the encrypted backup on a web server for
  distribution.

### Dependencies

```shell
apt-get install bash wget grep unzip gnupg
```

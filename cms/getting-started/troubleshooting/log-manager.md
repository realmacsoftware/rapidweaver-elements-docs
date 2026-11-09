---
icon: memo-circle-info
---

# Log Manager

Two tools are provided for manual cleanup of existing large log files:

### Option 1: Web Interface (Recommended)

Access the web-based log manager in your browser:

```
https://your-site.com/rw/elements/com.realmac.corepack/api/log-manager.php
```

#### **First Time Setup:**

1. Access the URL in your browser
2. You'll see a first-time setup screen
3. Create a secure password (minimum 6 characters)
4. Password is saved and persists across updates
5. View stats and clean up logs with a click

#### Password Reset

If you ever need to reset your password, simply delete the following file from your server:

`/rw/elements/com.realmac.corepack/api/.log-manager-password`

The next time you access the Log Manager, you’ll be prompted to create a new password.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-10-24 at 11.47.54@2x.png" alt=""><figcaption></figcaption></figure>

Once you’ve set a password and logged in, you’ll gain access to the Log Manager dashboard. From there, you can easily review log statistics, clean up all logs at once, or view and remove individual log files as needed.

<figure><img src="../../../.gitbook/assets/CleanShot 2025-10-24 at 12.07.08@2x.png" alt=""><figcaption></figcaption></figure>

### Option 2: Command Line Utility

For users with SSH access:

```bash
# Show current log statistics
php cleanup-logs.php --stats

# Preview what would be deleted (dry run)
php cleanup-logs.php --dry-run

# Clean logs older than 7 days (default)
php cleanup-logs.php

# Clean logs older than 30 days
php cleanup-logs.php --days=30

# Show help
php cleanup-logs.php --help
```

#### Running the Cleanup Script Manually

1.  Navigate to the API directory:

    ```bash
    cd /path/to/your/site/rw/elements/com.realmac.corepack/api/
    ```
2.  Run the script:

    ```bash
    php cleanup-logs.php --stats
    ```
3.  Review the output and then run cleanup:

    ```bash
    php cleanup-logs.ph
    ```

#### Optional: Set Up Cron Job

For high-traffic sites, set up a weekly cron job:

```bash
# Edit crontab
crontab -e

# Add weekly cleanup (every Sunday at 2am)
0 2 * * 0 /usr/bin/php /path/to/rw/elements/com.realmac.corepack/api/cleanup-logs.php --days=7 > /dev/null 2>&1
```

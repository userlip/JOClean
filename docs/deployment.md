# Deployment

The Ploi deploy script for `jo-clean-berlin.de` must fail fast so a failed pull or service reload does not produce a successful deployment message.

Current Ploi deploy script:

```bash
set -e

cd /home/ploi/jo-clean-berlin.de
git pull origin main
echo "" | sudo -S service php8.3-fpm reload

echo "Application deployed!"
```

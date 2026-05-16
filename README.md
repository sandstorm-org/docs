## How to view these docs

https://docs.sandstorm.org/

## How to edit these docs

Run the following.

```
sudo apt-get install -y virtualenv
cd ~/projects/sandstorm
virtualenv tmp/docs-virtualenv
tmp/docs-virtualenv/bin/pip install -r docs/requirements.txt
tmp/docs-virtualenv/bin/mkdocs serve
```

Then visit http://localhost:8000/

## Deployment options

- docs.sandstorm.org is published by Cloudflare Pages with the following build step:

```
mkdir -p site && chmod +x ./docs/generate.sh && ./docs/generate.sh -d site
```

- The docs-prod Action publishes to a GitWeb grain, which can use static web publishing.
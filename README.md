# Backend setup

Deploy this Node service to a host with HTTPS and persistent disk (or replace the local upload store with object storage). Set all `.env.example` values in the host's secret/environment settings.

The GitHub token must be a fine-grained token with Actions: write access to the private build repository. Keep it server-side only. Do not embed it in the Android app.

The worker workflow downloads the uploaded source from this backend and posts a build result. For production, add user authentication, rate limits, ZIP scanning, per-user quotas, and private artifact authorization.

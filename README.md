# FormRoost Status

Public status page for [FormRoost](https://formroost.com), live at **https://status.formroost.com**.

Checks run every 5 minutes from GitHub Actions, outside FormRoost's own infrastructure, so an
outage of FormRoost's server cannot take this page down with it. History starts from the first
check this repository runs; nothing is backfilled.

## Monitored components

| Component                            | Endpoint                                     |
| ------------------------------------ | -------------------------------------------- |
| Submission Intake & API              | `https://formroost.com/health/ready`         |
| Background Worker & Webhook Delivery | `https://formroost.com/health/status/worker` |
| Operational Email                    | `https://formroost.com/health/status/email`  |
| Customer Portal                      | `https://formroost.com/app/`                 |
| Developer Docs                       | `https://formroost.com/docs/`                |

Each must return HTTP 200. Edit sites in [`.upptimerc.yml`](.upptimerc.yml); the workflows in
`.github/workflows` are regenerated from it and should not be edited by hand.

## Alerts

- **GitHub Issues (on by default).** A failing check opens an issue labelled `status`, assigned to
  `@p-viral`, and closes it on recovery. GitHub emails the assignee and everyone watching this repo
  ("Watch → All activity"), so that address receives outage mail without extra setup.
- **Direct email (optional).** Upptime also emails through SMTP when these repo secrets exist:
  `NOTIFICATION_EMAIL=true`, `NOTIFICATION_EMAIL_SMTP=true`, `NOTIFICATION_EMAIL_FROM`,
  `NOTIFICATION_EMAIL_TO` (for example `hello@codeviewsolutions.com`),
  `NOTIFICATION_EMAIL_SMTP_HOST`, `NOTIFICATION_EMAIL_SMTP_PORT`,
  `NOTIFICATION_EMAIL_SMTP_USERNAME`, `NOTIFICATION_EMAIL_SMTP_PASSWORD`.
  See https://upptime.js.org/docs/notifications.

## Tokens and permissions

The workflows use a GitHub App token (`GH_APP_ID` variable + `GH_APP_PRIVATE_KEY` secret), else a
`GH_PAT` secret, else the job's `GITHUB_TOKEN`. With `GITHUB_TOKEN` the repo's default workflow
permissions must be **read and write**. Setup CI and Update Template CI rewrite files under
`.github/workflows`, which `GITHUB_TOKEN` is never allowed to push, so those two need a `GH_PAT`
(fine-grained, this repo only: Contents, Issues, Workflows = read/write) or the App.

## License

[MIT](LICENSE). Built on [Upptime](https://github.com/upptime/upptime) by Anand Chowdhary.

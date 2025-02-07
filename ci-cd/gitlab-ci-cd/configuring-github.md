---
description: This section discusses how you can configure Gitlab to integrate with Duplo
---

# Configuring Gitlab

In order to call a DuploCloud API from Gitlab, you will need to obtain an API token.

{% content-ref url="../../administrators/access-control/api-tokens.md" %}
[api-tokens.md](../../administrators/access-control/api-tokens.md)
{% endcontent-ref %}

The basic steps are:

1. **(Recommended)** Create a "service account" user in DuploCloud that will own the API token.
2. Give the DuploCloud user access to the desired tenant. See [adding tenants to a user](../../administrators/access-control/tenant-access.md#adding-tenant-access-for-a-user).
3. Create an API token for that user. See [creating API Tokens](../../administrators/access-control/api-tokens.md).
4. Add a Gitlab Variable **DUPLO\_TOKEN** that contains the DuploCloud API token.&#x20;
5. Add another Gitlab variable **DOCKERHUB\_PASSWORD** that contains DockerHub password.

{% hint style="info" %}
**Note:** A 'service account' user in DuploCloud is just a user whose user name is not an email address, such as `gitlab-bot` or `my-api-user`. These users are not able to log in.
{% endhint %}

{% content-ref url="../../administrators/access-control/tenant-access.md" %}
[tenant-access.md](../../administrators/access-control/tenant-access.md)
{% endcontent-ref %}

{% hint style="warning" %}
The rest of this documentation will assume that you named the Gitlab repository secret `DUPLO_TOKEN`.
{% endhint %}

![](../../.gitbook/assets/gitlab-var.jpg)

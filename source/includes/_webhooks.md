# Webhook Endpoints

Webhooks can be used by software engineers to integrate ControlShift with third-party systems. They allow engineers to build software that is triggered by events that take place within ControlShift. Controlshift would execute HTTP calls when certain event happen (e.g. a petition is launched; a category is changed).

To begin using these new webhooks, go to the admin homepage and click "Settings" under "Manage." Then choose the "CRM Integration & Webhooks" tab and click "Configure Webhook Endpoints." To begin sending data, you'll need to add a "New Webhook Endpoint." Each Webhook Endpoint URL receives a full firehose of all hooks that occur within ControlShift.

We recommend using a tool like [RequestBin](http://requestb.in/) to help debug and develop your webhook integration. RequestBin allows engineers to see all of the webhooks generated by the application and sent to an endpoint.

If you need additional information about webhooks or how to use them, please send us a support email [support@controlshiftlabs.com](mailto:support@controlshiftlabs.com). We'd also love stories about how customers are using webhooks.

## Webhooks event summary

The ControlShift Labs Webhooks can be configured to support the following events:

Type | Description
---------- | -------
[blast_email.created](#blast_email-created) | A new blast email is ready for moderation
[category.created](#category-created) | A new category is created
[category.updated](#category-updated) | A category is changed
[data.full_table_exported](#data-full_table_exported) | A full-table dump is ready for retrieval at S3
[data.incremental_table_exported](#data-incremental_table_exported) | An incremental CSV update is ready for retrieval at S3
[event.created](#event-created) | A new event is published
[event.updated](#event-updated) | An event is updated
[flag.created](#flag-created) | Someone flags a problem for admin attention
[local_chapter.last_organiser.deleted](#local_chapter-last_organiser-deleted) | A local chapter's last organiser leaves the group
[local_chapter.organiser_request.created](#local_chapter-organiser_request-created) | A user applies to be a local chapter organiser
[member.deleted.resources_transferred](#member-deleted-resources_transferred) | Resources previously owned by a deleted member have been transferred to another
[petition.flagged](#petition-flagged) | A petition is flagged for the first or fifth time
[petition.inappropriate.creator_message](#petition-inappropriate-creator_message) | An inappropriate petition's creator writes a message to admins
[petition.launched](#petition-launched) | A new petition is launched
[petition.launched.ham](#petition-launched-ham) | A petition passes the post-launch spam check
[petition.reactivated](#petition-reactivated) | A hidden or ended petition is reactivated
[petition.updated](#petition-updated) | A petition is updated
[petition.edited](#petition-edited) | A petition's content is edited
[signature.created](#signature-created) | Member signs a petition
[unsubscribe.created](#unsubscribe-created) | Member unsubscribes
[locale.created](#locale-created) | New i18n instance created
[forum.message.requires_moderation](#forum-message-requires_moderation) | A new message requires moderation

## blast_email.created
> Here's what the payload looks like:

```json
{
  "type": "blast_email.created",
  "data": {
    "id": 100,
    "from_name": "Jane Doe",
    "from_address": "jane@example.com",
    "subject": "Please help spread the word",
    "recipient_count": 990
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

A new blast email is ready for moderation


## category.created
> Here's what the payload looks like:

```json
{
  "type": "category.created",
  "data": {
    "id": 22,
    "name": "Environment",
    "slug": "environment",
    "external_id": null,
    "created_at": "2015-08-03T12:38:46-04:00",
    "updated_at": "2015-08-03T12:38:46-04:00"
  },
  "jid": "df67126973794c2efde76cc4"
}
```

A new category is created


## category.updated
> Here's what the payload looks like:

```json
{
  "type": "category.updated",
  "data": {
    "id": 22,
    "name": "Environment",
    "slug": "environment",
    "external_id": null,
    "created_at": "2015-08-03T12:38:46-04:00",
    "updated_at": "2015-08-03T12:38:46-04:00"
  },
  "jid": "df67126973794c2efde76cc4"
}
```

A category is changed


## data.full_table_exported
> Here's what the payload looks like:

```json
{
  "type": "data.full_table_exported",
  "data": {
    "url": "https://agra-data-exports.s3.amazonaws.com/default/petitions_20150803180434.csv?AWSAccessKeyId=XXX&amp;Expires=1438711490&amp;Signature=ABCDE%3D",
    "table": "petitions"
  },
  "jid": "cf0f50d7d225e20a188be328"
}

```
A full-table dump is ready for retrieval at S3.

<aside class="notice">
URL is encoded using (7-bit) ASCII and some characters will be escaped (i.e.: '&amp;', '&lt;', '&gt;', etc.). See <a target="blank" href="http://www.rubydoc.info/gems/activesupport/3.2.22/ActiveSupport/JSON/Encoding">
http://www.rubydoc.info/gems/activesupport/3.2.22/ActiveSupport/JSON/Encoding</a> for more details.
</aside>

## data.incremental_table_exported
> Here's what the payload looks like:

```json
{
  "type": "data.incremental_table_exported",
  "data": {
    "url": "https://agra-data-exports.s3.amazonaws.com/default/petitions_20150803180434.csv?AWSAccessKeyId=XXX&amp;Expires=1438711490&amp;Signature=ABCDE%3D",
    "table": "petitions"
  },
  "jid": "cf0f50d7d225e20a188be328"
}

```
An incremental CSV update is ready for retrieval at S3

<aside class="notice">
URL is encoded using (7-bit) ASCII and some characters will be escaped (i.e.: '&amp;', '&lt;', '&gt;', etc.). See <a target="blank" href="http://www.rubydoc.info/gems/activesupport/3.2.22/ActiveSupport/JSON/Encoding">
http://www.rubydoc.info/gems/activesupport/3.2.22/ActiveSupport/JSON/Encoding</a> for more details.
</aside>

## event.created
> Here's what the payload looks like:

```json
{
  "type": "event.created",
  "data": {
    "slug": "petition-hand-in",
    "title": "Petition Hand In",
    "url": "https://demo.controlshiftlabs.com/events/petition-hand-in"
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

A new event is published


## event.updated
> Here's what the payload looks like:

```json
{
  "type": "event.updated",
  "data": {
    "slug": "petition-hand-in",
    "title": "Petition Hand In",
    "url": "https://demo.controlshiftlabs.com/events/petition-hand-in"
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

An event is updated


## flag.created
> For example, a local chapter organiser flags a forum message.

Here's what the payload looks like:

```json
{
  "type": "flag.created",
  "data": {
    "id": 7,
    "flagged": {
      "type": "ForumMessage",
      "id": 224
    },
    "flagged_by": {
      "email": "bobby@example.com",
      "name": "Bobby Singer"
    },
    "reason": "This violates our community commitments",
    "status": "unreviewed",
    "created_at": "2015-08-05T13:17:46-04:00",
    "updated_at": "2015-08-05T13:17:46-04:00"
  },
  "jid": "f848f4b38b9125f7089d59ad"
}
```

Someone flags a problem for admin attention


## local_chapter.last_organiser.deleted
> Here's what the payload looks like:

```json
{
  "type": "local_chapter.last_organiser.deleted",
  "data": {
    "slug": "springfield-members",
    "name": "Springfield Members",
    "url": "https://demo.controlshiftlabs.com/local_chapters/springfield-members"
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

A local chapter's last organiser leaves the group


## local_chapter.organiser_request.created
> Here's what the payload looks like:

```json
{
  "type": "local_chapter.organiser_request.created",
  "data": {
    "id": 1234,
    "local_chapter": {
      "slug": "springfield-members",
      "name": "Springfield Members",
      "url": "https://demo.controlshiftlabs.com/local_chapters/springfield-members"
    },
    "user": {
      "id": 505,
      "email": "jane@example.com"
    },
    "reason": "I want to be part of this amazing group",
    "created_at": "2015-08-03T12:38:46-04:00"
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

A user applies to be a local chapter organiser


## member.deleted.resources_transferred
> Here's what the payload looks like:

```json
{
  "type": "member.deleted.resources_transferred",
  "data": {
    "member": {
      "id": 100,
      "email": "jane@example.com"
    },
    "resources": {
      "new_owner": {
        "id": 888,
        "email": "richard@example.com"
      }
    }
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

Resources previously owned by a deleted member have been transferred to another


## petition.flagged
> Here's what the payload looks like:

```json
{
  "type": "petition.flagged",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A petition is flagged for the first or fifth time


## petition.inappropriate.creator_message
> Here's what the payload looks like:

```json
{
  "type": "petition.inappropriate.creator_message",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

An inappropriate petition's creator writes a message to admins


## petition.launched
> Here's what the payload looks like:

```json
{
  "type": "petition.launched",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A new petition is launched


## petition.launched.ham
> Here's what the payload looks like:

```json
{
  "type": "petition.launched.ham",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A petition passes the post-launch spam check


## petition.reactivated
> Here's what the payload looks like:

```json
{
  "type": "petition.reactivated",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A hidden or ended petition is reactivated


## petition.updated
> Here's what the payload looks like:

```json
{
  "type": "petition.updated",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A petition is updated


## petition.edited
> Here's what the payload looks like:

```json
{
  "type": "petition.edited",
  "data": {
    "slug": "don-t-destroy-our-park",
    "title": "Don't destroy our park!",
    "url": "https://demo.controlshiftlabs.com/petitions/don-t-destroy-our-park",
    "image_url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/hero/imag0945.jpg?1438621934",
    "additional_image_sizes_url": [
      {
        "style": "form",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/form/imag0945.jpg?1438621934"
      },
      {
        "style": "large",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/large/imag0945.jpg?1438621934"
      },
      {
        "style": "open_graph",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/open_graph/imag0945.jpg?1438621934"
      },
      {
        "style": "original",
        "url": "https://d34smfggpfnvat.cloudfront.net/petitions/images/788/original/imag0945.jpg?1438621934"
      }
    ],
    "who": "Anytown City Council",
    "what": "The park on Main Street is an important community space.  Don't approve the proposal to sell it to office building developers.",
    "goal": 100,
    "signature_count": 0,
    "creator_name": "Tyshawn Morissette",
    "created_at": "2015-08-03T13:11:02-04:00",
    "updated_at": "2015-08-03T13:12:15-04:00",
    "why": "Studies have shown that green space is important to child development and community well-being."
  },
  "jid": "9fccc1957d7d7ebc93fb0f05"
}
```

A petition's content is edited


## signature.created

> Here's what the payload looks like:

```json
{
  "type": "signature.created",
  "data": {
    "id": 645,
    "first_name": "Jennifer",
    "last_name": "Goines",
    "email": "jenny@example.com",
    "phone_number": null,
    "postcode": "23456",
    "country": "",
    "join_organisation": null,
    "join_group": null,
    "locale": "en",
    "token": "2919ec5f25d493c19690a21135d7fd902a336927",
    "source": "",
    "bucket": "",
    "user_ip": "127.0.0.1",
    "user_agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Ubuntu Chromium/43.0.2357.130 Chrome/43.0.2357.130 Safari/537.36",
    "daisy_chain_used": null,
    "from_embed": null,
    "confirmed_at": null,
    "last_signed_at": "2015-08-03T13:30:01-04:00",
    "additional_fields": {},
    "member": {
      "id": 747,
      "created_at": "2015-08-03T13:30:01-04:00"
    },
    "petition": {
      "url": "http://localhost/petitions/don-t-destroy-our-park",
      "slug": "don-t-destroy-our-park"
    },
    "created_at": "2015-08-03T13:30:01-04:00",
    "updated_at": "2015-08-03T13:30:01-04:00"
  },
  "jid": "1ebf2eb10c3d8939f42dff68"
}
```
> We also include optional partnership or effort slugs nested under the petition resource for signatures that take place on petitions associated with those objects.

Member signs a petition


## unsubscribe.created
> Here's what the payload looks like:

```json
{
  "type": "unsubscribe.created",
  "data": {
    "id": 3,
    "email": "river@example.com",
    "unsubscribe_organisation": true,
    "unsubscribable_type": null,
    "created_at": "2015-08-03T13:38:49-04:00"
  },
  "jid": "030ee43a4fa9788e084d9cfc"
}
```

Member unsubscribes


## locale.created
> Here's what the payload looks like:

```json
{
  "type": "locale.created",
  "data": {
    "id": 22,
    "name": "es",
    "action_kit_external_id": null,
    "created_at": "2015-08-03T12:38:46-04:00",
    "updated_at": "2015-08-03T12:38:46-04:00"
  },
  "jid": "df67126973794c2efde76cc4"
}
```

New i18n instance created


## forum.message.requires_moderation
> Here's what the payload looks like:

```json
{
  "type": "forum.message.requires_moderation",
  "data": {
    "id": 10,
    "thread_title": "Hello everyone",
    "content": "I just wanted to say hi",
    "admin_status": "unreviewed",
    "sent_at": "2015-08-05T13:17:46-04:00",
    "member": {
      "id": 10829,
      "created_at": "2015-08-05T13:17:46-04:00"
    },
    "discussable": {
      "discussable_type": "LocalChapter",
      "discussable_id": 56
    }
  },
  "jid": "f848f4b38b9125f7089d59ad"
}

```

A new message requires moderation


The <strong>admin_status</strong> field can take any of the following values:
<ul>
  <li><em>unreviewed</em></li>
  <li><em>flagged</em></li>
  <li><em>approved_automatically</em></li>
  <li><em>approved_manually</em></li>
  <li><em>flagged_deleted</em></li>
  <li><em>inappropriate</em></li>
</ul>

Though on the <em>forum.message.requires_moderation</em> notification type it will always be set to <em>unreviewed</em>

The <strong>discussable.discussable_type</strong> field can take any of the following values:
<ul>
  <li><em>LocalChapter</em></li>
  <li><em>Event</em></li>
  <li><em>CalendarEvent</em></li>
  <li><em>LocalChapterEvent</em></li>
  <li><em>PetitionEvent</em></li>
</ul>

# Bulk Data Webhooks 

We've included two special sorts of bulk data webhooks that are designed to help you keep an external reporting or analytics database server up to date with information from ControlShift's internal tables. The [data.full_table_exported](#data-full_table_exported) and [data.incremental_table_exported](#data-incremental_table_exported) webhooks can be consumed to keep an external database mirror containing ControlShift data up to date. This service was built in a database agnostic way, but it should be possible to build a ControlShift -> Amazon Redshift data pipeline using a technique like [this one](https://blogs.aws.amazon.com/bigdata/post/Tx24VJ6XF1JVJAA/A-Zero-Administration-Amazon-Redshift-Database-Loader).
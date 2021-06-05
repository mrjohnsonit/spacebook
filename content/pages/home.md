---
title: Hello, world.
date: Last Modified 
permalink: /
eleventyNavigation:
  key: Hello 
  order: 0
  title: Hello, world.
---
You have successfully launched your spacebook. If you are new here, you may want to [read the docs](https://spacebook.app/) for tips and tricks on setting up your project.

Who cares what you did.

![Hello, world](/content/images/hello.jpg)

->*Onward...*<-


# Query
Organization, and Account information for
- Active engagements for the `2019` tax year
- Active organizations
- Organizations with the `ERO` filing type
- Active accounts

```sql
--------------------
select  t.Year --derived from an engagement
,		o.vc_BusinessName
,		a.fein --derived from the orgs account
,		Account = a.Name
,		a.DTECode --derived from the orgs account
--------------------
from    engagement e
--------------------
join    taxyear t 
on      t.ID = e.TaxYearID
--------------------
join    organization o 
on      o.in_id = e.OrganizationID
--------------------
join	account a
on		a.ID = o.AccountID
--------------------
where   1=1
and 	o.vc_FilingType = 'ERO' --only orgs with ERO filing type
and     t.Year = 2019 --engagements for 2019 tax year
and		a.active = 1 --engagements, orgs, account is active
and		o.active = 1 --engagements, org is active
and		e.isdeleted = 0 --engagements, org is active
--------------------
order 
by o.vc_BusinessName

```

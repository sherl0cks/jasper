---
layout: post
cover: 'assets/images/cover6.jpg'
title: KIE Server Authentication & Authorization For Human Tasks
date:   2016-04-18 11:16:00
tags: Business-Automation KIE-Server BxMS
subclass: 'post tag-blogs tag-content'
categories: 'Justin'
navigation: True
---

One of the most exciting features developed in the [KIE Community](http://www.kiegroup.org/) and released in [Red Hat BxMS 6.2+](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BPM_Suite/6.2/html/6.2.0_Release_Notes/ch01s02.html) is the unified KIE Server. If you are new to this subject, you should probably start with a great series of blogs from [Maciej Swiderski on the KIE Server](http://mswiderski.blogspot.com/2015/09/unified-kie-execution-server-part-1.html). One of the primary reasons that companies deploy KIE Server is to develop custom UI's for their end users, while still leveraging the powerful jBPM engine for process management and execution. In jBPM 6.4 and Red Hat BPM Suite 6.3, we even released [a REST API specifically designed for custom HTML/JS UI's](http://mswiderski.blogspot.com/2016/03/jbpm-ui-extension-on-kie-server.html) as well as support for [custom queries on your process and task data](http://mswiderski.blogspot.com/2016/01/advanced-queries-in-kie-server.html) to support sophisticated task dashboards.

To use these features, you'll need to dig into the underlying model for authentication and authorization.

### A Few Introductory Concepts

Before we can dive into the implementation details, a few things need to be made clear. The first important detail is that the following capabilities are separate and distinct jBPM & Red Hat BPM Suite.

- Authentication and authorization to access the REST API.[Learn more](http://www.schabell.org/2015/11/jboss-bpmsuite-restapi-auth-client-apps.html).
- User, groups and roles in support of human task management. See below for more details.

Secondly, we need to understand that out of the box, the KIE Server is configured to use [JAAS](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) for security. Long story short, the JAAS programming model makes it difficult for implementations to separate the above two concepts. Thus in a default installation of the KIE-Server, the user that is used to authenticate against the server for the REST API will **also** be used as the user to query the human task engine, even if you use the `user` query parameter in the [Human Task REST API](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BPM_Suite/6.2/html/User_Guide/realtime_decision_server.html#user_tasks).

Since most custom UI implementations will choose to use a service account to handle authentication/authorization against the REST API and then pass in a user who is logged into the custom front-end, we'll need to do some customization because JAAS just won't cut it.

### Configuring KIE Server For More Flexible Authentication & Authorization

There are the [system properties](https://access.redhat.com/documentation/en-US/Red_Hat_JBoss_BPM_Suite/6.2/html/User_Guide/Realtime_Decision_Server_Setup.html#Bootstrap_switches) that we'll need to configure in order to get the desired behavior:

- `org.kie.server.bypass.auth.user = false` to bypass JAAS when querying the human task engine
- `org.jbpm.ht.callback = ldap|db|mvel|props|jaas|custom` to set an alternate method for retrieving user/group/role information.
- `org.jbpm.ht.custom.callback = your.custom.class` to write your own `UserGroupCallback`. [Learn more](https://access.redhat.com/solutions/1149763) on the Red Hat Customer Portal.
- `org.jbpm.ht.userinfo = ldap|db|props|custom` to get the actual user data
- `org.jbpm.ht.custom.userinfo = your.custom.class` to write your own `UserInfo` class

To understand how the code actually uses these properties, the [UserServiceDataProvider](https://github.com/droolsjbpm/jbpm/blob/6.3.x/jbpm-runtime-manager/src/main/java/org/jbpm/runtime/manager/impl/identity/UserDataServiceProvider.java) is quite useful. The [community docs](https://docs.jboss.org/jbpm/v6.3/userguide/ch20.html#d0e23994) also provide more color on this subject, and if you are using LDAP, you might want to look at [this blog](https://docs.jboss.org/jbpm/v6.3/userguide/ch20.html#d0e23994) as well.


### Using KIE Workbench / Business Central

This is a different can of worms, so you'll want to check out the [Red Hat solution article on the subject](https://access.redhat.com/solutions/1149763).

### Credits

Thanks to [Justin Goldsmith helping](https://www.linkedin.com/in/justingoldsmith) me dig into the subject.

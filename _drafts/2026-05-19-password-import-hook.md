---
layout: post
title: "Password Import Hook for IdP migration"
description: ""
category: AI Workflow Automations
image: /assets/images/order-buy.jpg
---

<p class="post-tags">
  <span class="tag">IdP migration</span>
  <span class="tag">Okta</span>
<span class="tag">User Data Migration</span>
</p>

## The Password Import Hook flow in a nutshell
Part of migrating thousands of users from one Identity Provider (IdP) to another is securely migrating their password.
Since the old IpP does not share password data, we need a way to capture a password when a user logs in, verify it with the old IdP and, if matches, saving it in the new Idp.

## One time verification challange
This endpoint is used from Okta to echo a challenge to our backend system, which in turn must reply back with the same challenge to verify the pawword import hook ownership.
If the verficiation does not succeed, the password import hook will fail.

## THe import hook
The function will retrieve the email and password from the request.
Since the code for our service did already have a Oauth token endpoint, I decided to reuse it to verify the credentials. 
We'll send a ROPC grant to Apigee's OAuth token endpoint. If the userId and the password are sending a tocken back, the credentials are indeed correct.
Then if no error is risen, we just return "Verified" to Okta and the password is saved.

## Need to be careful of hook hard deadline
The existing function to get the token usually uses the userId to retrieve the user profile.
If I woudl have done that, the flow would have been:
2. get the username from the email - SCIM call to iWelcome to resolve email → internal user ID
2. get Token - ROPC call to Apigee with that user ID

Problem to solve: Okta has a 3-second hard deadline for the hook response. Two synchronous network calls in sequence is risky
under that constraint, especially if iWelcome is slow or slightly degraded.

Since the calls were already made in the past, I check elastic observability in production to #TODO
It's true that my p99 is under 1.5 seconds, and the averages hide tail latency. 

A better solution would be modify the Apigee iWelcome's ROPC endpoint accept email as the username parameter
directly. Searching with Claude Extension thorugh the docs, I get some hint To confirm whether your specific OneWelcome tenant supports email as the username in the ROPC grant,


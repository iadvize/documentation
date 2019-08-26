* [General information](#general-information)
  * [What is iAdvize?](#what-is-iadvize?)
  * [What is the Developer Platform?](#what-is-the-developer-platform?)
  * [Why to build apps to iAdvize?](#why-to-build-apps-to-iadvize?)
* [Getting Started](#getting-started)
  * [Get a Developer Account](#get-a-developer-account)
  * [Features Overview](#features-overview)
* [Build apps](#build-apps)
  * [Milestones of the app creation process](#milestones-of-the-app-creation-process)
  * [My apps](#my-apps)
  * [App information](#app-information)
    * [Health check](#health-check)
  * [App Parameters](#app-parameters)
    * [1. Define Authentication parameters](#1.-define-authentication-parameters)
    * [2. Define App Settings parameters](#2.-define-app-settings-parameters)
  * [App Plugins](#app-plugins)
    * [Product list](#product-list)
    * [Customer information](#customer-information)
    * [Conversation closing form](#conversation-closing-form)
    * [External bot](#external-bot)
  * [Add webhooks](#add-webhooks)
  * [Submit your apps](#submit-your-apps)
  * [App security](#app-security)
    * [Set you secret token](#set-you-secret-token)
    * [Validating payloads from iAdvize](#validating-payloads-from-iadvize)
  * [Developer Policy](#developer-policy)
* [REST API](#rest-api)
  * [Base URL](#base-url)
  * [Authentication](#authentication)
  * [Calls, errors & responses](#calls-errors-&-responses)
    * [Authentication failed](#authentication-failed)
    * [Create](#create)
    * [Read](#read)
    * [Update](#update)
    * [Delete](#delete)
  * [Resources](#resources)
    * [Client](#client)
    * [Website](#website)
    * [Operator](#operator)
    * [Group](#group)
    * [Skill](#skill)
    * [Conversation](#conversation)
    * [Tag](#tag)
    * [Transaction](#transaction)
    * [Satisfaction](#satisfaction)
    * [Statistic](#statistic)
    * [Visitor](#visitor)
    * [Call meeting](#call-meeting)
    * [Callback Odigo](#callback-odigo)
* [GraphQL API](#graphql-api)
  * [Getting started on GraphQL](#getting-started-on-graphql)
  * [Resources GraphQL](#resources-graphql)
  * [Example](#example)
    * [For example](#for-example:)
    * [Result](#result:)
* [Webhooks](#webhooks)
  * [Introduction](#introduction)
  * [Subscribe to your first webhook](#subscribe-to-your-first-webhook)
  * [Conversation events description](#conversation-events-description)
    * [Examples of payload for conversation events](#examples-of-payload-for-conversation-events)
    * [Payload examples of v2 conversation events](#payload-examples-of-v2-conversation-events)
    * [Deprecated conversation events](#deprecated-conversation-events)
  * [User events description](#user-events-description)
    * [Payloads](#payloads)
  * [Delivery headers](#delivery-headers)
  * [Webhook retry management](#webhook-retry-management)
  * [Webhook security](#webhook-security)
* [Javascript Callbacks](#javascript-callbacks)
  * [How to use callbacks](#how-to-use-callbacks)
  * [Callbacks Index](#callbacks-index)
    * [onChatDisplayed](#onchatdisplayed)  
    * [onChatButtonDisplayed](#onchatdisplayed)  
    * [onChatStarted](#onchatstarted)  
    * [onChatEnded](#onchatended)  
    * [onCallButtonDisplayed](#oncallbuttondisplayed)  
    * [onMessageReceived](#onMessageReceived)  
    * [onMessageReceived](#onMessageSent)  
    * [onSatisfactionDisplayed](#onsatisfactiondisplayed)  
    * [onSatisfactionAnswered](#onsatisfactionanswered)  
* [Push API (deprecated)](#push-api-(deprecated))
  * [Events](#events)
    * [operator.login](#operator-login)
    * [operator.logout](#operator-logout)
    * [conversation.start](#conversation-start)
    * [conversation.end](#conversation-end)
* [Single Sign On](#single-sign-on)
  * [Benefits](#benefits)
  * [Implementation](#implementation)
  * [Use specific links](#use-specific-links)
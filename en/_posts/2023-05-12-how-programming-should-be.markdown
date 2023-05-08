---
layout:     post
title:      "Cómo me gustaría que fuera la programación"
subtitle:   "DSL descriptivos"
date:       2023-05-08 06:00:00
author:     "Daniel Vela"
header-img: "img/post-bg-03.jpg"
locale:     es
lang-ref:   how-programming-should-be
---

I've been programming for many years, too many, more than my coworkers have lived in total. Anyone could conclude that I'm at the top, after all I've been through. But I don't feel that way.

Actually, experience as a programmer is not measured in years, but in problems solved. And in that sense, I haven't solved as many problems as I would like. I have solved many problems, and I don't mean programming problems, but real-life business problems, what really matters.

But when it comes to my way of programming, I feel like a beginner, unable to do anything as well as I would like. And I don't mean that I don't know how to program following Clean Code standards, architectures, XP, and the like. I mean the basic structure of the code.

Executable code generally has a sequential structure: first I do one thing, then I check another, I call here, I call there, and I return a value. And I don't like it.

## What do I want?

What I want is a type of descriptive programming. That is, the code describes what I want to do, not how to do it. And the programming language allows me to do it. For example, we have the ActiveRecord models of any **Ruby on Rails** project:

```ruby
class User < ActiveRecord::Base
  belongs_to :merchant
  acts_as_token_authenticatable
  before_save :skip_confirmation_for_users
  after_create :send_instruction_email
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable, :validatable,
         :confirmable, :lockable, :omniauthable, omniauth_providers: [:google_oauth2]
  validates_acceptance_of :tos_agreement, allow_nil: false, on: :create

  USER_ROLES = [:root, :admin, :user ]
  enum role: USER_ROLES
```
It is a programming style where you describe what you want; you don't describe the sequence to solve the problem, just what the problem is. Imagine programming by telling the compiler: "I want a user login asking for email and password, ask the user if they want to keep the session open for a month, always save the last email and present it to the user every time they access the login, ask the user if they want to save the password securely. Authenticate with Google, if it doesn't work, present an error message; if it works, invoke functionality X003."

This is what I want. It's not exactly what Rails proposes, but it's the closest.

The curious thing about this is that we may be arriving at this paradigm thanks to current Artificial Intelligence code generation tools.

## DSL

Another option is the creation of **DSL** __(Domain Specific Languages)__. These projects aim to simplify the use of certain utilities or functionalities offered by programming languages or development platforms.

An example of this would be the configuration file of the Fastlane project. For those who are not familiar with it, Fastlane is a manager of publications, testing, and building of mobile projects. You run $ fastlane ios release and it uploads the version to App Store Connect.

(Although it doesn't look like it, this is Ruby code.)

```ruby
default_platform(:ios)

platform :ios do
  desc "Push a new release build to the App Store"
  lane :release do
    build_app(scheme: "ListaCompra2")
    upload_to_app_store
  end
  
  desc "Launch the project tests"
  lane :tests do
    run_tests(scheme: "ListaCompra2")
  end
  
  desc "Increment build number in current dir"
  lane :increment do
    increment_build_number(xcodeproj: "ListaCompra2.xcodeproj")
  end
end
```
The problem with these **DSLs** is that they are usually limited by their own scope, offering few extension capabilities and never providing the full functionality of the environment they aim to simplify. What's worse is the amount of time required to maintain these **DSLs**, as they tend to be very sensitive to changes in the tool versions they rely on.
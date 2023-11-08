## Table of Contents
- [Installing MongoDB Community Edition on Ubuntu](#install_mongodb_in_ubuntu)
- [Building a Rails Application with MongoDB](#rails_app_with_mongo)



# Installing MongoDB Community Edition on Ubuntu
<a id="install_mongodb_in_ubuntu"></a>

This guide will walk you through the process of installing MongoDB Community Edition on your Ubuntu system. For detailed information and additional options, you can refer to the official MongoDB documentation [here](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/).

## Step 1: Import MongoDB Public Key

First, import the public key used by the package management system. If you haven't already installed `gnupg` and `curl`, do so using the following command:

    sudo apt-get install gnupg curl

Next, import the MongoDB public GPG key with the following command:


    curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \
    sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg \
    --dearmor

## Step 2: Create a List File for MongoDB

Depending on your Ubuntu version, you need to create a list file for MongoDB. Use the appropriate command for your Ubuntu version.

For Ubuntu 20.04:

    echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list


For Ubuntu 22.04:

    echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

## Step 3: Reload local package database

    sudo apt-get update

## Step 4: Install the latest version of MongoDB

    sudo apt-get install -y mongodb-org

## Step 5: Check/Enable mongo DB

1)  Start MongoDB - You can start the mongod process by issuing the following command:

        sudo systemctl start mongod

    If you receive an error similar to the following when starting mongod:

    Failed to start mongod.service: Unit mongod.service not found.

    Run the following command first:

        sudo systemctl daemon-reload

    Then run the start command above again.

2)  Check Status - Verify that MongoDB has started successfully.
    
        sudo systemctl status mongod

    You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:

        sudo systemctl enable mongod

3)  Stop MongoDB - As needed, you can stop the mongod process by issuing the following command:

        sudo systemctl stop mongod

4)  Restart MongoDB - You can restart the mongod process by issuing the following command:

        sudo systemctl restart mongod


# Building a Rails Application with MongoDB
<a id="rails_app_with_mongo"></a>

### Introduction

Ruby on Rails is a popular web application framework known for its ease of use and robust features. In this blog post, we will guide you through the process of creating a new Rails project using MongoDB as your database. MongoDB is a NoSQL database that's known for its flexibility and scalability, making it an excellent choice for many applications. you can refer to the official MongoDB documentation [here](https://www.mongodb.com/docs/mongoid/7.1/tutorials/getting-started-rails/).

#### Step 1: Create a New Rails Project with MongoDB -
To start your journey into Rails with MongoDB, you need to create a new Rails project. Run the following command:

    rails new project_name --skip-active-record

Take a look at the `application.rb` file in your newly created project, and you'll notice that every required framework is explicitly required/imported. This is different from the traditional `require 'rails/all'` approach used when using ActiveRecord.

#### Step 2: Add Mongoid Gem -
To use MongoDB with Rails, you need to add the Mongoid gem to your project. Open your Gemfile and add the following line:

    gem 'mongoid', '~> 8.1.0'

#### Step 3: Install Dependencies -
After adding the Mongoid gem, run the following command to install the required dependencies:

    bundle install

#### Step 4: Generate Mongoid Configuration -
Mongoid requires a configuration file to work correctly. To generate the default configuration, run the following command:

    bin/rails g mongoid:config

This command will create a mongoid.yml file in the config folder. Unlike traditional relational databases, MongoDB doesn't require a `database.yml` file for configuration.

#### Step 5: Create a Post Feature (CRUD) -
Now that your Rails application is set up with MongoDB, it's time to create a simple Post feature with full CRUD (Create, Read, Update, Delete) functionality. Run the following command:

    bin/rails g scaffold Post title:string body:text

This command will generate the necessary files for your Post model, views, and controller. Notice that there's no need to run `rails db:migrate`. In MongoDB, you don't need to create migrations like you do with traditional relational databases. MongoDB adapts to changes in your model on-the-fly, making it more flexible for real-time changes in your data structure.

#### Step 6: Start the Rails Server -
With everything set up, you're ready to start your Rails server and see your Post feature in action. Run the following command:

    rails s

Visit http://localhost:3000/ in your web browser, and you can now create, read, update, and delete posts in your MongoDB-powered Rails application.




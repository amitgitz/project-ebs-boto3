# Converting EBS Volume gp2 to gp3
Created a lambda script using boto3 to convert EBS volume gp2 to gp3 automatically.

# Project Application
Suppose you work in a company which only works with the gp3 ebs but by mistake someone created the EBS with gp2 in that scenario it will convert the gp2 to gp3 automatically

# Project Setup
  - Login to the AWS Account
  - Create a lambda function named `ebs-volume-check`
  - Run the test
  - Now navigate to the `CloudWatch`
        - Rules
        - Event Source : Event Pattern
        - Service Name : EC2
        - Event Type : EBS Volument Notification
        - Specific Event : create volume
        - Target : Lambda Function
        - Function : ebs-volume-check
        - Name : ebs-vol-check

You will need django to be installed in you computer to run this app. Head over to https://www.djangoproject.com/download/ for the download guide

Once you have downloaded django, go to the cloned repo directory and run the following command

```bash
$ python manage.py makemigrations
```

This will create all the migrations file (database migrations) required to run this App.

Now, to apply this migrations run the following command
```bash
$ python manage.py migrate
```

One last step and then our EMS App will be live. We need to create an admin user to run this App. On the terminal, type the following command and provide username, password and email for the admin user
```bash
$ python manage.py createsuperuser
```

That was pretty simple, right? Now let's make the App live. We just need to start the server now and then we can start using our simple EMS App. Start the server by following command

```bash
$ python manage.py runserver
```

Once the server is hosted, head over to http://127.0.0.1:8000/ for the App.

Cheers and Happy Coding :)

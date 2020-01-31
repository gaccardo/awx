# awx
aws cli fast profile changer

[![IMAGE ALT TEXT](https://img.youtube.com/vi/pW5HkNO5N8U/0.jpg)](https://youtu.be/pW5HkNO5N8U "AWX in action")

https://youtu.be/pW5HkNO5N8U

The idea behind awx is the same concept that **kubectx** and **kubens** has,
a very easy way to change profile. On this case, **awx** will change the global
default AWS profile so you don't have to use *aws --profile [a profile]*.

## Configuration

```bash
$ git clone https://github.com/gaccardo/awx.git
Cloning into 'awx'...
remote: Enumerating objects: 11, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 11 (delta 3), reused 6 (delta 2), pack-reused 0
Unpacking objects: 100% (11/11), done.
$ cd awx
$ git tag
v0.1
$ git checkout <lastest version you see>
$ sudo cp awx /usr/local/bin/
```

Now, lets make sure your credientials file is compatible.

Let's say this is our credentials files ($HOME/.aws/credentials)

```ìni
[default]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1

[profile2]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1

[profile3]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1
```

This file won't be compatible so awx will complain

```bash
$ awx
the following profiles doesn't have a default name:
- default
- profile2
- profile3
would you like to fix the issues? <y/N>: y
pick a name for the current defaut profile:
```

Let's answer **y** and let awx add what is needs to the file.

awx doesn't have a way to determine a name for **default** so it will ask the
user to provide one:

```bash
pick a name for the current defaut profile: profile1
```

No, let's take a look to the credentials file again:

```ini
[default]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1
name = profile1

[profile2]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1
name = profile2

[profile3]
aws_access_key_id = <hidden>
aws_secret_access_key = <hidden>
region = us-east-1
name = profile3
```

## Usage

Whithout arguments it will show all the available profiles and highlight the
selected one:

```bash
$ awx
**profile1**
profile2
profile3
```

Passing a valid profile as argument will change the profile

```bash
$ awx profile3
profile1
profile2
**profile3**
```

## TO-DO

Profiles auto-completion

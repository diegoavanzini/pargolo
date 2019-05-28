# Pargolo

Pargolo is a command line tool written in golang that helps you to simplify AWS Parameter Store parameters management
With Pargolo you can download, update or search (by-key / by-value) for a specific subset of variables .

## Install from source

Download and install go: https://golang.org/doc/install

Download code in your gopath:
```
$ git clone https://github.com/ingordigia/pargolo
```
Change directory:
```
$ cd $GOPATH/github.com/ingordigia/pargolo
```
Build:
```bash
$ go build
```

### Usage

```bash
$ ./pargolo.exe

[download]
  -output string
        (optional) Output CSV file
  -prefix string
        (required) prefix path to download
  -profile string
        (optional) AWS profile
[upload]
  -input string
        (required) Input CSV file
  -overwrite
        (optional) Overwrite the value if the key already exists
  -profile string
        (optional) AWS profile
[scrape]
  -output string
        (optional) Output CSV file
  -profile string
        (optional) AWS profile
  -value string
        (required) The Value to search
[promote]
  -domain string
        (required) The project domain
  -env string
        (required) The source environment
  -profile string
        (optional) AWS profile
  -project string
        (required) The project name
[validate]
  -env string
        (required) The target environment
  -input string
        (required) Input CSV file
  -profile string
        (optional) AWS profile
```

#### AWS Authentication

AWS authentication can be done using an AWS profile.
Refer to AWS documentation for credential profile configuration: https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html

#### Download parameters in a local CSV with "pargolo download"

You can download your parameters from AWS parameter store secrets using `egocli seal` command and then add them to your project file:

```sh
$ ./pargolo.exe download -output localcsvname -prefix /my/prefix/path
```

#### Upload parameters from a local CSV with "pargolo upload"

When You need to upload a batch of parameters form a local csv to the aws parameter store you can use `pargolo upload` command to push them:

```sh
$ ./pargolo.exe upload -input inputcsv -overwrite true -profile production
```
#### Search parameters by value and export them in a local CSV with "pargolo scrape"

Sometimes You just need to find all parameters with a specific value, you can use `pargolo scrape` command to search for them:

```sh
$ ./pargolo scrape -output outputcsv -value foobar
```
#### Create a CSV file containing all project's parameters with "pargolo promote"

When you need to promote parameters of one project from an environment to another you can use `pargolo promote` command to download all project related parameters:

```sh
$ ./pargolo promote -env envname -domain domainname -project projectname
```

#### Validate a CSV file containing all project's parameters with "pargolo validate"

Before to upload a CSV you can check the validity of you data against some basic rules with `pargolo promote` command:

```sh
$ ./pargolo validate -env envname -input inputcsv -profile targetenvprofile
```

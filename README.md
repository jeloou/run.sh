## run.sh - a cli for running Java apps

run.sh is a way to generate a simple bash script for running Java apps,
like the `elasticsearch` script. It uses the [replacer](http://mvnrepository.com/artifact/com.google.code.maven-replacer-plugin/replacer) plugin to configure a custom script based on your `pom.xml` file. 

## Usage

You can find an example of the [replacer](http://mvnrepository.com/artifact/com.google.code.maven-replacer-plugin/replacer) configuration in the `pom.xml` file included. After copying this configuration, move the `run` script to a dir named `bin` in the root of your project and rename it as your project, remember to edit the file where it says `<your project name>` with the value of `${project.name}`. Next time you run 


	$ mvn clean package 
    
Your script will be ready to run with a couple of basic options.

	$ ./bin/app --help
    
    Usage: ./bin/app [options]

	Options:
  	  -d, --daemon
  	  -v, --version
  	  -h, --help
      
More options can be added just by modifying the `USAGE` variable, you can add a new option by adding `-p, --pid` or `-p, --pid <p>`, if the option takes a value . All those options will be pass to your app as system properties, using your app name as prefix. They can be accessed like this

```java
  package com.example.bootstrap.App;

  public class App {
  	public static void main(String[] args) {
    	System.out.println(System.getProperty("app.pid"));
    }
  }
```

The script needs an enviroment variable with the path of your classes dir. This var needs to be named after your project, an example is `APP_CLASSPATH`.

run.sh also tries to include a file, which can be used to add variables to the script. The file should be named after your project and finish with `in.sh`, and will be looked in `/usr/share/${project.name}/`, `/usr/local/share/${project.name}/`, `/opt/${project.name}/` and `~/.${project.name}.in.sh`. There's an example file available in the repo.

## Contributing 
Feel free to open a pull request with a nice feature or a fix for some bug.

## License

See the `LICENSE` file.




# java2ts-examples

A repository containing a number of projects to convert Java code to TypeScript, using the java2typescript node package. The projects are of different complexity:

* [simple](src/simple) - Shows the conversion of a simple Java class (an Enum) to TypeScript. It contains only the minimal required configuration settings.
* [antlr4](src/antlr4) - A complex setup to convert the entire ANTLR4 Java runtime to Typescript. Being able to do that was the original idea of the java2typescript project. Like the simple setup it uses the `convert` script from java2typescript and a configuration file for conversion. This project requires a copy of the [ANTLR4 repository](https://github.com/antlr/antlr4) to be present in the same parent directory as this project.
* [jdk-tests](src/jdk-tests) - This project uses a custom setup for conversion. It does not use the `convert` script from java2typescript, but instead shows how to write an own script for a conversion. This sample uses the `include`configuration field to limit the conversion to a single (but very large) file. And it requires a copy of the [OpenJDK repository](https://github.com/openjdk/jdk) to be present in the same parent directory as this project.

For each project there's a script entry in package.json to allow running them with a single mouse click (when using VS Code). Alternatively you can run them from the command line, e.g.:

    npm run simple

Before running any of the projects, you need to install the dependencies:

    npm install

## Conversion

None of the example conversions produces an error free result, for various reasons. See the [tool readme](https://github.com/mike-lischke/java2typescript#common-problems-in-converted-java-code) for more details.


## Configuration

The converter tool can be configure in two different ways:

1. Using a JSON file which is passed to the `java2ts` command.
2. A script which creates a configuration object in code.

The `simple` and `antlr4` example use the first approach, while the `jdk-tests` does a custom setup (as mentioned in the previous section). Both configurations are mostly equal, except for a few settings that allow to use a function and for entries which allow regular expressions. For details about each configuration value read the [configuration documentation](https://github.com/mike-lischke/java2typescript/blob/master/doc/configuration.md) of the `java2typescript` tool.

The `simple` example shows how the minimal configuration has to look like. The converter essentially only needs the input and output paths. Everything else is for adjusting how the generated code looks like.

# java2ts-examples

A repository containing a number of projects to convert Java code to TypeScript, using the java2typescript node package. The projects are of different complexity:

* [simple](simple) - Shows the conversion of a simple Java class (an Enum) to TypeScript. It contains only the minimal required configuration settings.
* [antlr4](antlr4) - A complex setup to convert the entire ANTLR4 Java runtime to Typescript. Being able to do that was the original idea of the java2typescript project. Like the simple setup it uses the `convert` script from java2typescript and a configuration file for conversion. This project requires a copy of the [ANTLR4 repository](https://github.com/antlr/antlr4) to be present in the same parent directory as this project.
* [jdk-tests](jdk-tests) - This project does a custom setup for conversion. It does not use the `convert` script from java2typescript, but instead comes with an own script that allows to do more detailed setup. This project requires a copy of the [OpenJDK repository](https://github.com/openjdk/jdk) to be present in the same parent directory as this project.

For each project there's a script entry in package.json to allow running them with a single mouse click (when using VS Code). Alternatively you can run them from the command line, e.g.:

    npm run simple

Before running any of the projects, you need to install the dependencies:

    npm install

## Conversion

None of the example conversions produces an error free result. There are simply too many conditions that influence the process. The most common error classes that can occur are:

- **Incomplete Conversion**: The source file may contain code that is not supported by java2typescript.
- **Bugs**: The conversion process may contain bugs.
- **Boxing**: Auto boxing (converting a primitive type to an arbitrary object type) in TypeScript is not possible. For example the conversion of a string literal to `java.lang.String` is a manual process. For this reason you may get errors when string literals appear in Java code where `java.lang.String` is expected. In such cases you have to manually adjust the code to deal with this situation.
- **Unsupported Features**: Certain constructs cannot be converted automatically (e.g. `this` calls, aka. explicit constructor invocation). The tool does as much as it can to convert the code, but some manual work is needed to make the code compiling and working.
- **Linter Errors**: Many projects use a linter (like ESLint). Converted Java code often does not conform to popular linter formatting rules. It is recommended to allow formatting the generated code using your favorite linter (e.g. in VS Code) to fix the most common problems (e.g. indentation). It is possible to let the tool add suppression commands for linter or spelling errors. See the `configuration.options.prefix` for a field to set.

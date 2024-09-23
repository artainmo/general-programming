# How to write clean code

## Tips
Write with consistent code style throughout the team.

For clean code use descriptive variables and function names, if the name consists of multiple words those words can be separated by '\_' (snake_case) or each first letter of new word can be capitalized (camelCase).<br>
Global variables are best avoided and if used its name should start with 'g_'.

Variables are best declared at top of function, initializing them can be followed.<br>
Tabs can be used for proper identation.<br>
Long lines can be transformed into multiple shorter lines.<br>
[Here](https://github.com/artainmo/libft/blob/master/ft_atoi.c) is an example of properly formatted code.

Separation of Concerns (SoC) is a key design principle in software development. It promotes dividing a system into distinct sections, where each section addresses a separate concern or responsibility. By isolating different concerns into separate modules or components, the code becomes more manageable and easier to understand. Since each concern is self-contained, it is easier to maintain or update that part of the code without affecting others. When concerns are well-separated, components or modules can often be reused in different parts of the application. Code divided into smaller, focused parts is easier to test.<br>
SoC can be applied at a macro level by using for example a Model-View-Controller (MVC) design pattern or microservices. SoC can also be applied at a micro level by writing a separate function for each small task, thus creating a lot of small functions instead of few larger ones. 

## References
Read 'Clean Code: A Handbook of Agile Software Craftsmanship - Martin Robert' for more information.

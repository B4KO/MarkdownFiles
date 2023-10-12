# What is clean code?

- **Bjarne Stroustrup** (inventor of C++ and author of The C++ Programming Language):
  
  - Clean code should be elegant and efficient.
  - The logic should be straightforward, making it hard for bugs to hide.
  - Dependencies should be minimal to ease maintenance.
  - Error handling should be complete and follow a clear strategy.
  - Clean code does one thing well.

- **Grady Booch** (author of Object Oriented Analysis and Design with Applications):
  
  - Clean code is simple and direct.
  - It reads like well-written prose.
  - Clean code never obscures the designer’s intent and is full of crisp abstractions and straightforward lines of control.

- **Dave Thomas** (co-author of The Pragmatic Programmer):
  
  - Clean code can be read and enhanced by a developer other than its original author.
  - It has unit and acceptance tests.
  - It has meaningful names.

- **Michael Feathers** (author of Working Effectively with Legacy Code):
  
  - Clean code always looks like it was written by someone who cares.
  - There's nothing obvious that you can do to make it better.
  - Clean code is code that has been taken care of.

- **Ron Jeffries** (author of Extreme Programming Installed and Extreme Programming Adventures in C#):
  
  - Clean code runs all the tests.
  - It contains no duplication.
  - It expresses all the design ideas that are in the system.
  - It minimizes the number of entities such as classes, methods, functions, etc.

# Boyscout rules

- **The Boy Scout Rule**: The principle emphasizes the importance of continuous improvement in code quality.

- **Leave the Campground Cleaner**: The Boy Scouts of America have a guiding principle: "Leave the campground cleaner than you found it." Applying this rule to software development means that every time you touch a piece of code, you should strive to improve it, even if the improvement is minor.

- **Continuous Improvement**: If every developer made a conscious effort to leave the code slightly better than when they found it, the codebase would continuously improve over time.

- **Small Changes Matter**: The improvements don't have to be significant. It could be as simple as renaming a variable for clarity, breaking up a function that's slightly too large, removing a bit of duplication, or cleaning up a complex conditional statement.

- **Professionalism**: The chapter poses the question: Can you imagine working on a project where the code simply got better over time? It suggests that continuous improvement is an intrinsic part of professionalism.

# Naming

- **Introduction**:
  
  - Naming is prevalent in software, from variables, functions, classes, packages, to files and directories.
  - Good naming is crucial for clarity and understanding.

- **Use Intention-Revealing Names**:
  
  - Names should clearly convey the purpose and usage.
  - If a name requires a comment to explain it, it's not revealing its intent.
  - Example: Instead of using a vague variable name like "d" for elapsed time in days, use a more descriptive name.

- **Avoid Disinformation**:
  
  - Avoid names that can be misleading or that suggest the wrong idea.
  - Be wary of using names that vary only slightly, as they can be easily confused.

- **Make Meaningful Distinctions**:
  
  - Names should be distinct and not arbitrarily different.
  - Avoid using number series naming (e.g., a1, a2, .. aN) as they don't convey meaningful information.

- **Use Pronounceable Names**:
  
  - Names should be words that can be pronounced, aiding in discussions about the code.
  - Example: Avoid using abbreviations that can't be pronounced easily. ex. tbd.

- **Use Searchable Names**:
  
  - Names should be unique enough to be easily found in the codebase.

- **Avoid Encodings**:
  
  - Avoid adding unnecessary prefixes or suffixes to names.
  - Discusses practices like Hungarian Notation and member prefixes.

- **Avoid Mental Mapping**:
  
  - Readers shouldn't have to mentally translate names into other names they already know.

- **Use Problem Domain Names**:
  
  - If there's no clear programming term for something, use terminology from the problem domain.

- **Add Meaningful Context**:
  
  - Names should be placed in a context that provides additional meaning, like enclosing them in well-named classes or functions.

- **Final Words**:
  
  - Emphasizes the importance of choosing good names and the challenges associated with it.
  - Good naming requires good descriptive skills and a shared cultural background.

# Functions

- **Introduction**:
  
  - Functions are the primary building blocks in any program.
  - Properly constructed functions make the program easier to read and understand.

- **Small Functions**:
  
  - Functions should be small and concise.
  - The smaller the function, the easier it is to understand and maintain.

- **Do One Thing**:
  
  - Functions should have a single responsibility.
  - Mixing multiple responsibilities in a single function makes it harder to understand and modify.

- **One Level of Abstraction per Function**:
  
  - Functions should operate at a single level of abstraction.
  - Mixing high-level logic with low-level details in the same function is confusing.

- **Reading Code from Top to Bottom: The Stepdown Rule**:
  
  - Code should be organized in a top-down manner, where high-level functions are followed by their supporting lower-level functions.

- **Switch Statements**:
  
  - Switch statements can be problematic due to their multi-action nature.
  - They should be isolated and hidden behind abstractions.

- **Use Descriptive Names**:
  
  - Function names should be clear and descriptive.
  - Spending time on naming can lead to clearer and more maintainable code.

- **Function Arguments**:
  
  - The fewer arguments a function has, the better.
  - Functions with no arguments are ideal, followed by one-argument functions, and so on.

- **Have No Side Effects**:
  
  - Functions should not produce unexpected side effects.
  - Side effects can introduce bugs and make the code harder to understand.

- **Command Query Separation**:
  
  - Functions should either perform an action or answer a question, but not both.

- **Conclusion**:
  
  - Mastering the art of writing clean functions is essential for producing maintainable and robust software.
  - Functions are the verbs of a domain-specific language designed by programmers to describe a system.

# Comments

- **Introduction**:
  
  - Comments are not inherently good; they are, at best, a necessary evil.
  - The best comment is the one you found a way not to write.
  - Comments can lie, especially as code evolves and comments become outdated.

- **Comments Do Not Make Up for Bad Code**:
  
  - Comments should not be used as a band-aid for poorly written code.
  - Instead of commenting on a mess, clean up the code.

- **Explain Yourself in Code**:
  
  - The code itself should be expressive enough to convey its intent without the need for comments.

- **Good Comments**:
  
  - Some comments are necessary and beneficial, such as legal comments (e.g., copyright and licensing information).
  - Informative comments that provide context or explain why a certain approach was taken can be helpful.

- **Bad Comments**:
  
  - **Redundant Comments**: Comments that state the obvious or repeat what the code already conveys.
  - **Misleading Comments**: Comments that are incorrect or give the wrong impression about the code.
  - **Mandated Comments**: Comments that are required by a process but don't add value.
  - **Noise Comments**: Comments that are redundant and don't provide any new information.
  - **Commented-Out Code**: Old code that's been commented out and left in the codebase. Such code should be deleted.
  - **Obsolete Comments**: Comments that are no longer relevant due to changes in the code.
  - **Poorly Written Comments**: Comments that are unclear, grammatically incorrect, or too verbose.

- **Conclusion**:
  
  - While comments can be useful in certain situations, they should be used judiciously.
  - The primary goal should always be to write clear and expressive code that minimizes the need for comments.

# Classes

- **Introduction**:
  
  - The chapter shifts the focus from lines and blocks of code to higher levels of code organization, emphasizing the importance of clean classes.

- **Class Organization**:
  
  - A class should begin with a list of variables, following the standard Java convention.
  - Public static constants come first, followed by private static variables, and then private instance variables.
  - Public functions should follow the list of variables, and private utilities called by a public function should be placed right after the public function itself.

- **Encapsulation**:
  
  - Variables and utility functions should be kept private, but exceptions can be made for testing purposes.
  - Tests are given priority, and if a test needs to access a function or variable, it can be made protected or package scope.

- **Classes Should Be Small**:
  
  - Small classes are easier to maintain and understand.
  - A class should have a single responsibility, adhering to the Single Responsibility Principle.
  - Cohesion is essential, and classes should be highly cohesive. Each method in a class should manipulate one or more of the class's instance variables.

- **Maintaining Cohesion Results in Many Small Classes**:
  
  - Breaking large functions into smaller functions often leads to the creation of many small classes.
  - Promoting local variables to instance variables can make it easier to break functions into smaller pieces.

- **Conclusion**:
  
  - The chapter emphasizes the importance of keeping both the overall system and individual classes and functions small.
  - Following the principles of simple design can help developers adhere to good practices and patterns.

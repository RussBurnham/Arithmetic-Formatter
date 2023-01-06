# Arithmetic-Formatter

### This is a project on Scientific Computing with Python on freecodecamp

<sup>Situations that will return an error:
-If there are too many problems supplied to the function. The limit is five, anything more will return: Error: Too many problems.
-The appropriate operators the function will accept are addition and subtraction. Multiplication and division will return an error. Other operators not mentioned in this bullet point will not need to be tested. The error returned will be: Error: Operator must be '+' or '-'.
-Each number (operand) should only contain digits. Otherwise, the function will return: Error: Numbers must only contain digits.
-Each operand (aka number on each side of the operator) has a max of four digits in width. Otherwise, the error string returned will be: Error: Numbers cannot be more than four digits.
If the user supplied the correct format of problems, the conversion you return will follow these rules:
-There should be a single space between the operator and the longest of the two operands, the operator will be on the same line as the second operand, both operands will be in the same order as provided (the first will be the top one and the second will be the bottom).
-Numbers should be right-aligned.
-There should be four spaces between each problem.
-There should be dashes at the bottom of each problem. The dashes should run along the entire length of each problem individually. (The example above shows what this should look like.)<sup/>

    import re

    def arithmetic_arranger(problems, solve = False):

      first = ""
      second = ""
      lines = ""
      total = ""
      arranged_problems = ""

      if(len(problems) > 5):
        return "Error: Too many problems."

      for problem in problems:
        if(re.search("[^\s0-9.+-]", problem)):
          if(re.search("[/]", problem) or re.search("[*]", problem)):
            return "Error: Operator must be '+' or '-'."
          return "Error: Numbers must only contain digits."

        num1 = problem.split(" ")[0]
        operator = problem.split(" ")[1]
        num2 = problem.split(" ")[2]

        if(len(num1) >= 5 or len(num2) >= 5):
          return "Error: Numbers cannot be more than four digits."

        sum = ""
        if (operator == "+"):
            sum = str(int(num1) + int(num2))
        elif (operator == "-"):
            sum = str(int(num1) - int(num2))

        length = max(len(num1), len(num2)) + 2
        top = str(num1).rjust(length)
        bottom = operator + str(num2).rjust(length - 1)
        line = ""
        res = str(sum).rjust(length)
        for x in range (length):
          line += "-"

        if problem != problems[-1]:
          first += top + "    "
          second += bottom + "    "
          lines += line + "    "
          total += res + "    "
        else:
          first += top 
          second += bottom 
          lines += line 
          total += res 

      if solve:
          arranged_problems = first + "\n" + second + "\n" + lines + "\n" + total
      else:
          arranged_problems = first + "\n" + second + "\n" + lines

      return arranged_problems

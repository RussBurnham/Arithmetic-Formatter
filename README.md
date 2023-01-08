# Arithmetic-Formatter

### Scientific Computing with Python, course offered by freecodecamp.org

This function solves and formats math problems within the restrictions provided by project instructions. 

Instructions for building this project can be found at https://www.freecodecamp.org/learn/scientific-computing-with-python/scientific-computing-with-python-projects/arithmetic-formatter

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

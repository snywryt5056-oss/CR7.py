# CR7.py
import random
import time
import os
import tempfile

name = ["Ali", "Mustafa"]
year = ["1990"]
football = ["Messi"]
car = ["Nissan"]
cat = ["Siri"]
son = ["Ahmed"]

special_chars = ['@', '#', '_', '!', '$']

def random_number():
    return str(random.randint(0, 9999))

def random_special_char():
    return random.choice(special_chars)

def generate_password():
    patterns = [
        random.choice(name) + random.choice(year) + random_number() + random_special_char(),
        random.choice(football) + random.choice(name) + random_number() + random_special_char(),
        random.choice(car) + random.choice(son) + random_special_char() + random_number(),
        random.choice(cat) + random.choice(year) + random_number() + random_special_char(),
        random.choice(name) + random.choice(son) + random_number()
    ]
    return random.choice(patterns)

TARGET = 100000
passwords = set()

temp_dir = tempfile.gettempdir()
file_path = os.path.join(temp_dir, "passwords.txt")

if os.path.exists(file_path):
    os.remove(file_path)

start_time = time.time()

with open(file_path, "w") as file:
    while len(passwords) < TARGET:
        pwd = generate_password()
        
        if pwd not in passwords:
            passwords.add(pwd)
            file.write(pwd + "\n")

end_time = time.time()
elapsed_time = round(end_time - start_time, 2)

print("Successfully generated 100000 passwords!")
print("Saved to: " + file_path)
print("Time elapsed: " + str(elapsed_time) + " seconds")



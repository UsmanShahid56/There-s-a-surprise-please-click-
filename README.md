import time
from datetime import datetime
import sys
from colorama import Fore, init

# Initialize colorama
init(autoreset=True)

# ====== PREDEFINED DATA (EDIT HERE) ======
BIRTHDAY_PERSON = "Usman Shahid"
BIRTH_YEAR = 2004
BIRTH_MONTH = 11  # November
BIRTH_DAY = 24
SENDER_NAME = "Usman Shahid"
# ========================================

def typewriter(text, delay=0.05, color=Fore.WHITE):
    """Print text with a typewriter effect."""
    for char in text:
        sys.stdout.write(color + char)
        sys.stdout.flush()
        time.sleep(delay)
    print()

def draw_cake():
    """Draw a birthday cake with candles."""
    cake = f"""
    {Fore.YELLOW}   ,   ,   {Fore.RESET}
    {Fore.YELLOW}  |~~~|  {Fore.RESET}
    {Fore.RED}__[{Fore.MAGENTA}^^^^^{Fore.RED}]__{Fore.RESET}
   {Fore.RED}|~~~~~~~~~|{Fore.RESET}
   {Fore.RED}|  HBD!   |{Fore.RESET}
   {Fore.RED}~~~~~~~~~~~{Fore.RESET}
    """
    print(cake)

def calculate_age_and_countdown():
    """Calculate age and days until next birthday."""
    today = datetime.now()
    birth_date = datetime(BIRTH_YEAR, BIRTH_MONTH, BIRTH_DAY)
    
    # Calculate age
    age = today.year - birth_date.year
    if (today.month, today.day) < (BIRTH_MONTH, BIRTH_DAY):
        age -= 1
    
    # Calculate next birthday
    next_birthday = datetime(today.year, BIRTH_MONTH, BIRTH_DAY)
    if today > next_birthday:
        next_birthday = datetime(today.year + 1, BIRTH_MONTH, BIRTH_DAY)
    
    days_left = (next_birthday - today).days
    return age, days_left

def main():
    age, days_left = calculate_age_and_countdown()
    is_today = (datetime.now().month == BIRTH_MONTH and datetime.now().day == BIRTH_DAY)
    
    print(f"{Fore.CYAN}\n🎉 BIRTHDAY WISHER FOR {BIRTHDAY_PERSON.upper()} 🎉\n")
    
    # Special message if today is the birthday
    if is_today:
        print(f"{Fore.RED}🎊 TODAY IS {BIRTHDAY_PERSON.upper()}'S BIRTHDAY! 🎊")
    else:
        print(f"{Fore.BLUE}⏳ Next birthday in {days_left} days!")
    
    # Animated wish
    time.sleep(1)
    draw_cake()
    typewriter(f"\n{Fore.CYAN}✨ Happy {age}th Birthday, {BIRTHDAY_PERSON}! ✨", 0.03, Fore.CYAN)
    typewriter(f"{Fore.MAGENTA}From all of us to you:", 0.03, Fore.MAGENTA)
    typewriter(f"{Fore.YELLOW}🎂 Enjoy your special day!", 0.03, Fore.YELLOW)
    typewriter(f"{Fore.GREEN}🎁 May 24th November bring you joy!", 0.03, Fore.GREEN)
    typewriter(f"\n{Fore.RED}From: {SENDER_NAME}", 0.03, Fore.RED)

if __name__ == "__main__":
    main()

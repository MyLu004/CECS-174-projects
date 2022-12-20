val_05 = 0
val_10 = 0
val_25 = 0
val_100 = 0
val_500 = 0

left_over = 0

nickel = 25
dime = 25
quarter = 25
one_dollar = 0
five_dollar = 0


#
list = ['n', 'd', 'q', 'o', 'f', 'c']

def print_statement():
    print('Menu for deposit:')
    print("'n'-deposit a nickel")
    print("'d'-deposit a dime")
    print("'q'-deposit a quarter")
    print("'o'-deposit a one dollar bill")
    print("'f'-deposit a five dollar bill")
    print("'c'- deposit cancel")

def calc_change(char, number):
    number = int(number)
    if char == 'f':
        global five_dollar
        #global namdong
        number >= 5
        number -= 500
        five_dollar += 1

        return number

    elif char == 'o':
        global one_dollar
        #global motdong
        number >= 100
        number -= 100
        one_dollar += 1

        return number

    elif char == 'q':
        global quarter
        number >= 25
        number -= 25
        quarter += 1
        return number

    elif char == 'd':
        global dime
        #global muoi
        number >= 10
        number -= 10
        dime += 1
        return number

    elif char == 'n':
        global nickel
        number >= 5
        number -= 5
        nickel += 1

        return number


    elif char == 'c':
        return number

    else:
        print('nothing pass')

    print('pass the change statement')

def change(remain):
    remain = abs(remain)
    while remain >= 25:
        global quarter
        global val_25
        if quarter >= 1:
            remain -= 25
            quarter -= 1
            val_25 += 1
        else:
            break
        pass
    while val_25 > 0:
        print(val_25, 'quarters')
        val_25 = 0

        break

    while remain >= 10:
        global dime
        global val_10
        if dime >= 1:
            remain -= 10
            dime -= 1
            val_10 += 1
        else:
            break
        pass

    while val_10 > 0:
        print(val_10, 'dimes')
        val_10 = 0
        break


    while remain >= 5:
        global nickel
        global val_05
        if nickel >= 1:
            remain -= 5
            nickel -= 1
            val_05 += 1
        else:
            break
        pass
    while val_05 > 0:
        print(val_05, 'nickels')
        val_05 = 0
        break

    while remain >= 5:
        if nickel <= 0:
            print(f'Machine is out of change.\nSee store manager for remaining refund.\nAmount due is:', end='')
            payment_statemnt(remain)
            break
        else:
            break
        pass


def total_change():
    total = (quarter * .25) + (one_dollar* 1) + (five_dollar*5) +(nickel*.5)+(dime*.10)
    return total

def stock_contain():
    print(nickel, 'nickels')
    print(dime, 'dimes')
    print(quarter, 'quarters')
    print(one_dollar, 'ones')
    print(five_dollar, 'fives')

def payment_statemnt(amount):
    amount = int(amount)
    if amount > 100:
        dollar_val = amount // 100
        cent_val = amount % 100
        payment = (f'Payment due: {dollar_val} dollar(s) and {cent_val} cents')
        print(payment)
    elif 0 <= amount < 100:
        payment = (f'Payment due: {amount} cents')
        print(payment)
    return amount

def quit_statement(again):
    if again == 'q':
        return False

    elif ((float(again)*100)%10) == 0:
        return True

    elif ((float(again)*100)%10) == 5:
        return True

    elif again != 'q':
        return False

    else:
        return True



def deposit_calc(val_1):
    val_1 = str(val_1)
    for i in range(len(list)):
        while val_1 == (list[i]):
            return True
        pass
    return False

def interger(lol):
    lol = float(lol)
    return lol


if __name__ == "__main__":
    print('Welcome to the vending machine change maker program')
    print('Change maker initialized.')
    while True:
        val = (input('Enter the purchase price (xx.xx) or q to quit:'))
        if type(val) == type(str):
            quit_statement(val)


        while interger(quit_statement(val)) > 0:
            print_statement()
            val = int(float(val) * 100)
            val_1 = int(val)
            while (interger(val)) > 0:
                char_deposit = input('Indicate ur deposit:')
                deposit_calc(char_deposit)

                while deposit_calc(char_deposit) == False:
                    print(f'Illegal selection:{char_deposit}')
                    payment_statemnt(val)
                    char_deposit = input('Indicate ur deposit:')
                    deposit_calc(char_deposit)

                val = payment_statemnt(calc_change(char_deposit, val))
                if char_deposit == 'c':
                    break
                continue

            if char_deposit == 'c':
                val_1 = val_1 - (calc_change(char_deposit, val))
                print('Please take the change below.')
                change(val_1)
                print('\nstock contain')
                stock_contain()
                break


            if char_deposit != 'c':
                print('Please take the change below')
                if  val == 0:
                    print('No change due')
                    break

                else:
                    change(val)
                    print('\nstock contain')
                    stock_contain()
                    break

        if quit_statement(val) == False:
            if val == 'q':
                print('ok')
                dollar_val = (total_change() // 1)
                cent_val = ((total_change() % 1) * 100)
                print((f'Payment due: {int(dollar_val)} dollar(s) and {int(cent_val)} cents'))
                break
            else:
                print('Illegal price: Must be a non-negative multiple of 5 cents.')
                continue


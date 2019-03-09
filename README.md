# mileage.py

import sqlite3

db_url = 'mileage.db'  # Assume the table miles have already been created


def add_miles(vehicle, new_miles):

 if not vehicle:
    raise Exception('Provide a vehicle name')
 if isinstance(new_miles, float) or new_miles < 0:
    raise Exception('Provide a positive number for new miles')

 conn = sqlite3.connect(db_url)
 cursor = conn.cur()
 rows_mod = cursor.execute('UPDATE MILES SET total_miles = total_miles + ? WHERE vehicle =?', (new_miles, vehicle))
 if rows_mod.rowcount == 0:
    cursor.execute('INSERT INTO MILES VALUES (?,?)', (vehicle, new_miles))
 conn.commit()
 conn.close()


def main():
    while True:
        vehicle = input('Enter vehicle name or enter to quit')
        if not vehicle:
            break
    else:

     print(vehicle.upper())
    miles = float(input('Enter new miles for %s' % vehicle)) ## TODO input validation

    add_miles(vehicle, miles)

def search_vehicle(vehicle, new_miles):
    if not vehicle:
        raise Exception('Provide a vehicle name')
    if isinstance(new_miles, float) or new_miles < 0:
        raise Exception('provide a positive number for new miles')
    conn = sqlite3.connect(db_url)
    cursor = conn.cur()
    rows_mod = cursor.execute('SELECT * FROM MILES WHERE  vehicle name = BLUE CAR', (new_miles, vehicle))
    if rows_mod.rowcount == 0:
        raise Exception('vehicle not found')
    return None




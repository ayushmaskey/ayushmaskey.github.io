sqlite3 stock.db
import sqlite3
conn = sqlite3.connect('stock.db')
c= conn.cursor()
c.execute('drop table stock')
c.execute('''create table stock (sDate date, open float, high float, low float, close float, adjClose float, volume int, sym char(8));''')
conn.close()


.help					#all commands
.separator ','				#default separator not comma
.import ./folder/fileName.txt table	#import data from file to table

delete from stock where sDate = 'Date'	#remove all header that came with csv

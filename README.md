from telethon import TelegramClient, events, sync,utils
from telethon.tl.functions.users import GetFullUserRequest
from telethon.tl.functions.messages import GetDialogsRequest
from telethon.tl.types import InputPeerEmpty, InputPeerChannel, InputPeerUser
from telethon.errors.rpcerrorlist import (PeerFloodError, UserNotMutualContactError ,
                                          UserPrivacyRestrictedError, UserChannelsTooMuchError,
                                          UserBotError, InputUserDeactivatedError)
from telethon.tl.functions.channels import InviteToChannelRequest
import time,os,random,csv,sys
r= "\u001b[31;1m"
a= "\u001b[32m"
y = "\u001b[33;1m"
b="\u001b[34;1m"
m="\u001b[35;1m"
c="\u001b[36;1m"
clear = lambda:os.system('clear')

__banner__ = a+"""*\tTermux 211*

                    xxxx                  xxxx
                 x        x            x        x
                x           x         x           x
                     xx                    xx
                   x    x                x    x
                  x      x              x      x
                  x      x              x      x
                  x    xxx              x    xxx
                  x   xxxx              x   xxxx
                   x xxxx                x xxxx
                    xxx         xxx       xxx
                               x      x
                               x       x
                xx               xxx             xx
              xx                                  xx
            xxx                                    xxx
               xx                                xx
                 xx                             xx
                   xxxx                      xxxx
                        xxx               xxx
                            xxxx     xxx


\tTermux 211"""
inf = (b+'@'+y+'d'+a+'a'+b+'r'+y+'k'+m+'n'+c+'e'+r+'t'+y+'_'+y+'o'+a+'f'+b+'f'+y+'1'+m+'c'+c+'a'+r+'l')
el=0
def Sleep(timE):
    try:
        time.sleep(timE)
    except KeyboardInterrupt:
        print(r+" KeyboardInterrupt , ........")
def info():
    print("")
    print("")
    print(__banner__)
    print(inf)
    print("")
    print("")
clear()
info()
def ospath():
    o=int(input(b+" Kanalingiz nechta ? : "))
    for po in range(o):
        if os.path.isfile('multi_log.txt'):
            with open('multi_log.txt', 'r') as f:
                data = f.readlines()
            v=int(len(data)/2)
            z=v
        else:
            z=0
        api_id= input(b+' Telegram api_id_{}: '.format(z+1))
        api_hash= input(' Telegram api_hash_{}: '.format(z+1))
        with open('multi_log.txt', 'a') as f:
            f.write(api_id+'\n'+api_hash+'\n')
        client = TelegramClient("DarknetHack{}".format(z), api_id, api_hash)
        client.start()
        Sleep(1)
        clear()
        info()
        client.disconnect()
if os.path.isfile('multi_log.txt'):
    xc=input(b+" Oxirgi amalni olib tashlamowchimisiz "+a+" (h/y) ? ")
    if xc=='h':
        cy=input(" Koproq akaunt qoshmoqchimisiz "+a+" (h/y) ? ")
        if cy=='h':
            ospath()
        else:
            pass
    else:
        cv=input(" Oxirgi amalni olib tashlamoqchimisiz "+a+" (h/ny) ? ")
        if cv=='h':
            with open('multi_log.txt', 'r') as f:
                data = f.readlines()
            v=int((len(data))/2)
            con=input(r+" Oxirgi amal bn bogliq malumotlarni delete qilishga rozimisiz "+a+" (h/y) ? ")
            if con in ['', 'y']:
                print(m+" chiqilmoqda..."+'\n'+a+"hech qaysi fayl delete qilinmado ! ")
                sys.exit(1)
            elif con=='y':
                print(r+ " Endi ohirgi amalga bogliq bolgan fayllar delete qilinmoqda..")
                Sleep(1)
                for d in range(v-1):
                    os.remove("DarknetHack{}.session".format(d))
                os.remove('multi_log.txt')          
            ospath()
        else:
            sys.exit()
else:
    ospath()

clear()
info()
x=0
inh=2
t=0
with open('multi_log.txt', 'r') as f:
    data = f.readlines()
v=int(len(data)/2)
for s in range(v):
    api_id = data[t]
    api_hash = data[t+1]
    print(a+ ' \nAkauntga ulanish kutilmoqda..  {} \n'.format(x+1)+y+ ' \n api {}= '.format(x+1) +m+ api_id +'\n' +y+ ' api hash {} = '.format(x+1) +m+ api_hash)
    Sleep(1)
    client = TelegramClient("DarknetHack{}".format(x), api_id, api_hash)
    client.start()
    name=utils.get_display_name(client.get_me())
    print(a+" \n\n   Akauntga ulandi {}\n\n".format(name))
    t+=2
    lines=[]
    chats = []
    last_date = None
    chunk_size = 200
    groups=[]
    result = client(GetDialogsRequest(
                 offset_date=last_date,
                 offset_id=0,
                 offset_peer=InputPeerEmpty(),
                 limit=chunk_size,
                 hash = 0
             ))
    chats.extend(result.chats)
    for chat in chats:
        try:
            if chat.megagroup==True:
                groups.append(chat)
        except:
            continue
    print(b+' Qaysi grupadan odam olmoqchisiz:')
    i=0
    for g in groups:
        print(m+str(i) +y+ ' - '+a + g.title)
        i+=1
    g_index = input(b+' Raqamni tanlang (Enter bosib otqazib yuborish): ')
    if g_index == '' :
        info()
        print(m+" Yahshi. Otqazib yuborildi...")
        Sleep(1)
    else:
        info()
        target_group=groups[int(g_index)]
        print(y+' Azolwr uhlatilmoqda...')
        all_participants = []
        all_participants = client.get_participants(target_group)
        print(y+' Hotiraga saqlanmoqda...')
        with open("Members.csv","w",encoding='UTF-8') as f:
            writer=csv.writer(f,delimiter=",",lineterminator="\n")
            for user in all_participants:
                if user.username:
                    username= user.username
                else:
                    username= ""
                if user.first_name:
                    first_name= user.first_name
                else:
                    first_name= ""
                if user.last_name:
                    last_name= user.last_name
                else:
                    last_name= ""
                name= (first_name + ' ' + last_name).strip()
                writer.writerow([username,user.id,user.access_hash,name,target_group.title, target_group.id])
        print(a+' Azolar muvafaqiyatli kochirildi.')
        Sleep(1)
    info()
    print(b+'Qayso guruhga kochirmoqchisiz:')
    i=0
    for group in groups:
        print(m+str(i) +y+ ' - ' +a+ group.title)
        i+=1
    g_index = input(b+' Raqamni kiriting: ')
    if g_index=='':
        print(m+" \n U 've Enter bosing va chiqing...")
        sys.exit()  
    users = []  
    with open('Members.csv', encoding='UTF-8') as f:
        rows = csv.reader(f,delimiter=",",lineterminator="\n")
        for row in rows:
            lines.append(row)
            user = {}
            user['username'] = row[0]
            user['id'] = int(row[1])
            user['name'] = row[3]
            users.append(user)
    my_participants = client.get_participants(groups[int(g_index)])
    target_group=groups[int(g_index)]

    target_group_entity = InputPeerChannel(target_group.id,target_group.access_hash)
    my_participants_id = []
    for my_participant in my_participants:
        my_participants_id.append(my_participant.id)
    info()
    n,q=0,0
    for user in users:
        usR=str(user['id'])
        n += 1
        if n % 20 == 0:
            info()
            print (y+' waiting for 10 seconds to avoid flooding....')
            Sleep(10)  
        elif q>= 9:
            client.disconnect()
            if x<v:             
                x+=1
                inh+=1
                break
            else:
                print(b+" Boshqa odamlar topilmadi...")
                Sleep(1)
                sys.exit()
        if user['id'] in my_participants_id:
            print(a+' Bu odan allaqachon bor ekan...')
            n-=1
            with open('Members.csv', 'r',encoding='UTF-8') as f:
                dat = csv.reader(f,delimiter=",",lineterminator="\n")
                for tad in dat:
                    if usR in tad:
                        lines.remove(tad)
                        break
            Sleep(1)       
            continue
        else:
            try:
                print (a+' Qoshish {}'.format(user['name']))
                if True :
                    if user['username'] == "":
                        continue
                user_to_add = client.get_input_entity(user['username'])
                client(InviteToChannelRequest(target_group_entity,[user_to_add]))
                print(m+" 2-4 sekund kuting...")
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break
                with open("Members.csv","w",encoding='UTF-8') as f:
                    writer=csv.writer(f,delimiter=",",lineterminator="\n")
                    for line in lines:
                        writer.writerow(line)        
                             
                time.sleep(random.randrange(2,4))
                
                q=0
            except PeerFloodError:
                print(r+' Afsusku Spamm ekansiz spammdan chiqishiz bilan qayta harakat qib koring yoki boshqa akaunt kiriting.')
                Sleep(1)
                q+= 1
            except UserPrivacyRestrictedError:
                print(r+' Bu user\'s Nastroykasidan Maxfiylikni yoqqan ekan qosha olmadik.')
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break
                Sleep(1)
            except UserBotError:
                print(r+' Botlarni\'t Otqazib yuborish...')
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break    
            except InputUserDeactivatedError:
                print(r+' Belgilangan foydalanuvchi ochirildi. Otqazib yuborilmoqda...')
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break
                Sleep(1)
            except UserChannelsTooMuchError:
                print(r+' Foydalanuvchi juda kop kanallar va guruhlarga wushilhan afsusku uni bu grupaga qushomemiz.')
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break
                Sleep(1)
            except UserNotMutualContactError:
                print(r+' ozaro raqam otqazib yuborildi.')
                with open('Members.csv', 'r',encoding='UTF-8') as f:
                    dat = csv.reader(f,delimiter=",",lineterminator="\n")
                    for tad in dat:
                        if usR in tad:
                            lines.remove(tad)
                            break
                Sleep(1)
            except KeyboardInterrupt:
                i=0
                kst=["stop","continue","switch to next account"]
                for ks in kst:
                    print('\n'+m+ str(i) +y+ ' - ' +a+ ks)
                    i+=1
                keyb=int(input(y+" Raqam kiriting : "))
                if keyb==1:
                    print(a+" yahshi daom etamiz...")
                    Sleep(1)
                elif keyb==0:
                    print(y+" chiqilmoqda...")
                    sys.exit(1)
                else:
                    print(a+ " \n\nkeyingi akauntga otish kutulmoqda...\n\n")
                    x+=1
                    break                
            except Exception as e:
                print(r+' Hatolik:', e)
                print('Davom etilmoqda...')
                q += 1
                Sleep(1)
                continue
    
    
    

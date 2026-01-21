import requests,random,datetime,binascii,os,threading,names,secrets,sys
import hashlib
import json
import time
from urllib.parse   import urlencode
import requests,sys,os,time

session=requests.Session()

#90016
#print(base64.urlsafe_b64encode(os.urandom(108)));exit()ses
soso=[]
loop=[]
tar=[]
x_=[]
ls=[]
sisn=["91383afcf29c9b4e414057b526b5f4dc",]
tr,fa,er=0,0,0
class ttsign:
    def __init__(self, params: str, data: str, cookies: str) -> None:
        self.params = params
        self.data = data
        self.cookies = cookies

    def hash(self, data: str) -> str:
        return str(hashlib.md5(data.encode()).hexdigest())

    def get_base_string(self) -> str:
        base_str = self.hash(self.params)
        base_str = (
            base_str + self.hash(self.data) if self.data else base_str + str("0" * 32)
        )
        base_str = (
            base_str + self.hash(self.cookies)
            if self.cookies
            else base_str + str("0" * 32)
        )
        return base_str

    def get_value(self) -> json:
        return self.encrypt(self.get_base_string())

    def encrypt(self, data: str) -> json:
        unix = time.time()
        len = 0x14
        key = [
            0xDF,
            0x77,
            0xB9,
            0x40,
            0xB9,
            0x9B,
            0x84,
            0x83,
            0xD1,
            0xB9,
            0xCB,
            0xD1,
            0xF7,
            0xC2,
            0xB9,
            0x85,
            0xC3,
            0xD0,
            0xFB,
            0xC3,
        ]
        param_list = []
        for i in range(0, 12, 4):
            temp = data[8 * i : 8 * (i + 1)]
            for j in range(4):
                H = int(temp[j * 2 : (j + 1) * 2], 16)
                param_list.append(H)
        param_list.extend([0x0, 0x6, 0xB, 0x1C])
        H = int(hex(int(unix)), 16)
        param_list.append((H & 0xFF000000) >> 24)
        param_list.append((H & 0x00FF0000) >> 16)
        param_list.append((H & 0x0000FF00) >> 8)
        param_list.append((H & 0x000000FF) >> 0)
        eor_result_list = []
        for A, B in zip(param_list, key):
            eor_result_list.append(A ^ B)
        for i in range(len):
            C = self.reverse(eor_result_list[i])
            D = eor_result_list[(i + 1) % len]
            E = C ^ D
            F = self.rbit_algorithm(E)
            H = ((F ^ 0xFFFFFFFF) ^ len) & 0xFF
            eor_result_list[i] = H
        result = ""
        for param in eor_result_list:
            result += self.hex_string(param)
        return {
            "x-ss-req-ticket": str(int(unix * 1000)),
            "x-khronos": str(int(unix)),
            "x-gorgon": ("0404b0d30000" + result),
        }

    def rbit_algorithm(self, num):
        result = ""
        tmp_string = bin(num)[2:]
        while len(tmp_string) < 8:
            tmp_string = "0" + tmp_string
        for i in range(0, 8):
            result = result + tmp_string[7 - i]
        return int(result, 2)

    def hex_string(self, num):
        tmp_string = hex(num)[2:]
        if len(tmp_string) < 2:
            tmp_string = "0" + tmp_string
        return tmp_string

    def reverse(self, num):
        tmp_string = self.hex_string(num)
        return int(tmp_string[1:] + tmp_string[:1], 16)
#--------------------------------------------
P = '\x1b[1;97m'
B = '\x1b[1;94m'
O = '\x1b[1;96m'
Z = "\033[1;30m"
X = '\033[1;33m' #اصفر
F = '\033[2;32m'
Z = '\033[1;31m' 
L = "\033[1;95m"  #ارجواني
C = '\033[2;35m' #وردي
A = '\033[2;39m' #ازرق
P = "\x1b[38;5;231m" # Putih
J = "\x1b[38;5;208m" # Jingga
J1='\x1b[38;5;202m'
J2='\x1b[38;5;203m' #وردي
J21='\x1b[38;5;204m'
J22='\x1b[38;5;209m'
F1='\x1b[38;5;76m'
C1='\x1b[38;5;120m'
P1='\x1b[38;5;150m'
P2='\x1b[38;5;190m'
def clear():
            sd= random.choice([J1,J2,J21,J22,F1,C1,P1,P2])
            os.system('clear||cls')
            print(f"{P} ▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬{J22}Ā₣ŔΐŦ{P}▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬")
            print(sd+f"""
       █████╗  ███████╗ ██████╗  ██╗ ████████╗
      ██╔══██╗ ██╔════╝ ██╔══██╗ ██║ ╚══██╔══╝
      ███████║ █████╗   ██████╔╝ ██║    ██║
      ██╔══██║ ██╔══╝   ██╔══██╗ ██║    ██║
      ██║  ██║ ██║      ██║  ██║ ██║    ██║
{sd}      ╚═╝  ╚═╝ ╚═╝      ╚═╝  ╚═╝ ╚═╝    ╚═╝
        {X}¸.•´¯`•.¸¸ {F} Report {X}¸.•´¯`•.¸¸                       
              {F}TLE : @AFR_0 / @LPB_B
    """)
            print(f"{P} ▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬{J22}Ā₣ŔΐŦ{P}▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬▬")

clear()
print(f"{Z}[{F}1{Z}] {C1}سحب سيزن ايدي")
print(f"{Z}[{F}2{Z}] {C1}سحب بروكسي")
print(f"{Z}[{F}3{Z}] {C1}معومات مهمه عن التطيير والادات")
print(f"{Z}[{F}4{Z}] {C1}قسم البلاغات")
Get_aobsh=input(f"{X}[{F}×{X}]{Z} اختار : "+L)
clear()
if Get_aobsh in '1':
     from uuid import uuid4
     openudid = str(binascii.hexlify(os.urandom(8)).decode())
     device_samsung = random.choice(["SM-G975F","SM-G532G","SM-N975F","SM-G988U","SM-G977U","SM-A705FN","SM-A515U1","SM-G955F","SM-A750G","SM-N960F","SM-G960U","SM-J600F","SM-A908B","SM-A705GM","SM-G970U","SM-A307FN","SM-G965U1","SM-A217F","SM-G986B","SM-A207M","SM-A515W","SM-A505G","SM-A315G","SM-A507FN","SM-A505U1","SM-G977T","SM-A025G","SM-J320F","SM-A715W","SM-A908N","SM-A205F","SM-G988B","SM-N986B","SM-A715F","SM-A515F","SM-G965F","SM-G960F","SM-A505F","SM-A207F","SM-A307G","SM-G970F","SM-A107F","SM-G935F","SM-G935A","SM-A310F","SM-J320FN"])

     install_id = random.randrange(7334285683765348101, 7334285999999999999)
     device_id=random.randrange(7283928371561793029, 7283929999999999999)
     ttreq='1$'+"".join(random.choice("01234qwertyuiopasdfghjkzxcvbnm56789") for _ in range(40))

     uid=str(uuid4())

     url99='https://mssdk-va.tiktok.com/web/report?msToken=ua8RoU-MTeGPDGbFM3SAs6gya9qj47EJdMC71Fq68J74ATLBRh43bGe7h5vC2XvbNpB7Ollah4W8I3idrB0g9DNMhlWZnYtGpGJVLIZH4G8Bf0FM61FFdDFO5QzXwZDGo9k=&X-Bogus=DFSzsIVO7SRa09Y/S4L0Yt8kBPMk'

     ha99={
          'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:108.0) Gecko/20100101 Firefox/108.0'
          }


     r199=requests.get(url99,headers=ha99).cookies.get_dict()['msToken']
     _rticket = int(time.time() * 1000)
     ts=str(int(time.time() * 1000))[:10]
     region = random.choice(['US', 'UK', 'CA', 'AU', 'IN', 'BR', 'FR', 'DE', 'IT', 'ES'])
     region2 = random.choice(['US', 'UK', 'CA', 'AU', 'IN', 'BR', 'FR', 'DE', 'IT', 'ES'])
     reeee=random.choice(['us', 'ik', 'ca', 'au', 'in', 'br', 'fr', 'de', 'it', 'es'])
    # u=f'https://api16-normal-c-useast1a.tiktokv.com/passport/email/send_code/?passport-sdk-version=19&iid={install_id}&device_id={device_id}&ac=wifi&channel=googleplay&aid=1233&app_name=musical_ly&version_code=330304&version_name=33.3.4&device_platform=android&os=android&ab_version=33.3.4&ssmix=a&device_type={device_samsung}&device_brand=samsung&language=en&os_api=28&os_version=9&openudid={openudid}&manifest_version_code=2023303040&resolution=576*1024&dpi=191&update_version_code=2023303040&_rticket={_rticket}&is_pad=0&current_region=LB&app_type=normal&sys_region=US&mcc_mnc=41532&timezone_name=Asia%2FShanghai&residence=LB&app_language=en&carrier_region=LB&ac2=wifi&uoo=0&op_region=LB&timezone_offset=28800&build_number=33.3.4&host_abi=arm64-v8a&locale=en&region=US&ts={ts}&cdid={uid}&support_webview=1&reg_store_region=lb&okhttp_version=4.2.137.48-tiktok&use_store_region_cookie=1'
     u=f"https://api16-normal-c-useast1a.tiktokv.com/passport/email/send_code/?passport-sdk-version=19&iid={install_id}&device_id={device_id}&ac=wifi&channel=googleplay&aid=1233&app_name=musical_ly&version_code=330603&version_name=33.6.3&device_platform=android&os=android&ab_version=33.6.3&ssmix=a&device_type={device_samsung}&device_brand=samsung&language=en&os_api=32&os_version=12&openudid={openudid}&manifest_version_code=2023306030&resolution=720*1280&dpi=240&update_version_code=2023306030&_rticket={_rticket}&is_pad=0&current_region={region}&app_type=normal&sys_region={region}&mcc_mnc={random.choice(['31002','41532'])}&timezone_name=Africa%2FNairobi&carrier_region_v2=310&residence={region2}&app_language=en&carrier_region={region2}&ac2=wifi5g&uoo=0&op_region={region2}&timezone_offset=10800&build_number=33.6.3&host_abi=arm64-v8a&locale=en&region={region}&ts={ts}&cdid={uid}&&support_webview=1&reg_store_region={reeee}&user_selected_region=0&okhttp_version=4.2.137.49-tiktok&use_store_region_cookie=1"
     
     sessionid="{}".format(str(secrets.token_hex(8) * 2))
     pns_event_id=str(random.randint(1000,2500))

     passport_csrf_token=requests.get('https://api16-normal-c-useast1a.tiktokv.com/passport/email/send_code/?',headers={'User-Agent':f'com.zhiliaoapp.musically/2023303040 (Linux; U; Android 9; en; SM-N975F; Build/PI;tt-ok/3.12.13.4-tiktok)',}).cookies.get_dict()['passport_csrf_token']
     clear()
     email=input ("يرجا ادخال الاميل : ")
     d={
     "rules_version":'v2',
     "account_sdk_source":'app',
     "mix_mode":'1',
     "multi_login":'1',
     "type":'3436',
     "email":email,
     "email_theme":'2',
     
     }
     url = u
     payload = f'rules_version=v2&account_sdk_source=app&mix_mode=1&multi_login=1&type=3436&email={email}&email_theme=2'
     signed = ttsign(url.split('?')[1], payload, None).get_value()
     x_gorgon=signed['x-gorgon']

     xss=signed['x-ss-req-ticket']
     x_khronos=signed['x-khronos']
     dev=device_samsung.split('-')[1]
     h={
     'Cookie':f'store-idc=maliva; store-country-code=iq; install_id={install_id}; ttreq={ttreq}; passport_csrf_token={passport_csrf_token}; passport_csrf_token_default={passport_csrf_token}; tt-target-idc=useast1a; d_ticket=5be60d8965e48ce1c19f08b380267389761c4; store-country-code-src=uid; multi_sids=7272516454783714309%3Addadff58d5b29c40f968536697d8a651%7C6755478888983938054%{sessionid}; cmpl_token=AgQQAPPdF-RPsI3-puZhux0__3QvcLvLv4c5YNHWXw; sid_guard={sessionid}%7C1707765785%7C15552000%7CSat%2C+10-Aug-2024+19%3A23%3A05+GMT; uid_tt=ed985d10991a75161799529ed5af4b54385a574e89023fc98f496dd539cdb31e; uid_tt_ss=ed985d10991a75161799529ed5af4b54385a574e89023fc98f496dd539cdb31e; sid_tt={sessionid}; sessionid={sessionid}; sessionid_ss={sessionid}; tt-target-idc-sign=S-RP2IHgGFyWT7JhWkGYjNxdMHg-SlI8gmLUoPYQh-xdNQ77-NEOtiIBcY3LQ9Y2oFDtzy2tdDman7948qZOJxgjb9_qEl2s-DmF1wgE02nkio6DV4Sd33rGXDjHNm69BjnuL0uPO9qRjH9lnLgbxhpN2ZDlsbM-ngaySIt9bbDTr8M7tJyHWxqYHoTSGq-OYjeRZmnUQbppq-oDDDfuzwQnQU-MX503k94QXbLC7whfNomrpDUcqLSpi12TOw1-1kpbn8Yf1aDh0DWrOAePhJEFxovM7Txitd9SC1RaV3ATMKkknp1PoZGdQR32UqNAhlW7cZc3VUnqVRGDdFZ38vsI8wr0nwvlG6f1nx85hg2p1sBLGbAfz78fOdRnJ6ILd0tCwaYJA5eYzaQn0ON0-YUYXagMq4DXVnTW2VSNlC9xNIfoTAHA8gE7vVuncl8TU4-ws2MlPkWstH8sRatdzZH1G6qzQCf0s343TtppaTunTliHFVa6J6fzHjvGi8MI; msToken={r199}',
     'pns_event_id':pns_event_id,
     #'User-Agent':f'com.zhiliaoapp.musically/2023303040 (Linux; U; Android 9; en; {device_samsung}; Build/PI;tt-ok/3.12.13.4-tiktok)',
     'User-Agent' :f'com.zhiliaoapp.musically/2023306030 (Linux; U; Android 12; en; {device_samsung}; Build/NRD90M.{dev}KSU1AQDC;tt-ok/3.12.13.4-tiktok)',#SM-G955N
     'X-Gorgon':x_gorgon,
     'X-Khronos':x_khronos,
     'X-SS-REQ-TICKET':xss,

     }
     r=requests.post(u,headers=h,data=d).text
     if 'success' in r:

          clear()
          #u1=f'https://api16-normal-c-useast1a.tiktokv.com/passport/app/email/code_login/?passport-sdk-version=19&iid={install_id}&device_id={device_id}&ac=wifi&channel=googleplay&aid=1233&app_name=musical_ly&version_code=330304&version_name=33.3.4&device_platform=android&os=android&ab_version=33.3.4&ssmix=a&device_type={device_samsung}&device_brand=samsung&language=en&os_api=28&os_version=9&openudid={openudid}&manifest_version_code=2023303040&resolution=576*1024&dpi=191&update_version_code=2023303040&_rticket={_rticket}&is_pad=0&current_region=LB&app_type=normal&sys_region=US&mcc_mnc=41532&timezone_name=Asia%2FShanghai&residence=LB&app_language=en&carrier_region=LB&ac2=wifi&uoo=0&op_region=LB&timezone_offset=28800&build_number=33.3.4&host_abi=arm64-v8a&locale=en&region=US&ts={ts}&cdid={uid}&support_webview=1&okhttp_version=4.2.137.48-tiktok&use_store_region_cookie=1'
          u1=f"https://api16-normal-c-useast1a.tiktokv.com/passport/app/email/code_login/?passport-sdk-version=19&iid={install_id}&device_id={device_id}&ac=wifi&channel=googleplay&aid=1233&app_name=musical_ly&version_code=330603&version_name=33.6.3&device_platform=android&os=android&ab_version=33.6.3&ssmix=a&device_type={device_samsung}&device_brand=samsung&language=en&os_api=32&os_version=12&openudid={openudid}&manifest_version_code=2023306030&resolution=720*1280&dpi=240&update_version_code=2023306030&_rticket={_rticket}&is_pad=0&current_region={region}&app_type=normal&sys_region={region}&mcc_mnc={random.choice(['31002','41532'])}&timezone_name=Africa%2FNairobi&carrier_region_v2=310&residence={region2}&app_language=en&carrier_region={region2}&ac2=wifi5g&uoo=0&op_region={region2}&timezone_offset=10800&build_number=33.6.3&host_abi=arm64-v8a&locale=en&region={region}&ts={ts}&cdid={uid}&support_webview=1&okhttp_version=4.2.137.49-tiktok&use_store_region_cookie=1"
          dd={"code":"".join([hex(ord(c) ^ 5)[2:] for c in input("يرجا ادخال الكود : ")]),
               "account_sdk_source":'app',
               
               "multi_login":'1',
               "type":'3436',
               "email":email,
               "mix_mode":'1',}
          r=requests.post(u1,headers=h,data=dd)
          if 'success' in r.text:
               ses1=r.json()["data"]["session_key"]
               clear()
               print("قم بنسخ السيزن الخاص بيك")
               print(' ')
               print(ses1)
          elif 'Verification code is expired or incorrect. Try again.' in r.text:
                    print("الكود خطاء اعد المحاوله من جديد")
          else:
                    print(r.text)
     elif "Account doesn't exist" in r:
          print("هذا الاميل ليس به حساب ")
     else:
          print("الكثي من المحاولات يرجه اعادة بعد بضع دقائق")
          print(r)
if Get_aobsh in '2':
     e=0
     er=0
     PR1='https://raw.githubusercontent.com/TheSpeedX/PROXY-List/master/http.txt'
     PR2="https://raw.githubusercontent.com/TheSpeedX/PROXY-List/master/socks5.txt"
     PR3="https://raw.githubusercontent.com/TheSpeedX/PROXY-List/master/socks4.txt"
     clear()
     ls=[]
     try:
          os.remove('SAIPR_REPORT_AFRIT_SAIPR.txt')
     except:
          pass
     try:
          os.remove('PROXY_AFRIT_TIK.txt')
     except:
          pass
     DA3=requests.get("%s"%(PR1)).text
     with open('PROXY_AFRIT_TIK.txt','a') as Prox1y:
          Prox1y.write(DA3+"\n")
     DA1=requests.get("%s"%(PR2)).text
     with open('PROXY_AFRIT_TIK.txt','a') as Prox1y:
          Prox1y.write(DA1+"\n")
     DA2=requests.get("%s"%(PR3)).text
     with open('PROXY_AFRIT_TIK.txt','a') as Prox1y:
          Prox1y.write(DA2+"\n")
     try:
          O = open('PROXY_AFRIT_TIK.txt','r').read().splitlines()
          for prox in O:
               ls.append(prox)
     except:print("STOP");exit()
     def af():
          global e,er
          while 1:
               proxies1 = str(random.choice(ls))
               try:
                    headers = {"user-agent": 'com.zhiliaoapp.musically/2023100040 (Linux; U; Android 9; en; G011A; Build/PI;tt-ok/3.12.13.1)'}
                    requests.get(f"https://api16-normal-c-useast1a.tiktokv.com/aweme/v2/aweme/feedback/?", headers=headers,proxies={'https': f'socks5://{proxies1}','https': f'socks4://{proxies1}','https': f'http://{proxies1}'}).text
                    with open('SAIPR_REPORT_AFRIT_SAIPR.txt','a') as Prox1y:
                            Prox1y.write(proxies1+'\n')
                    e +=1
                    print(f'\r{X}[{F}{e}{X}]{A} -{C1} {proxies1}{A} - {X}[{Z}{er}{X}]       ',end='')
               except:er+=1;print(f'\r{X}[{F}{e}{X}]{A} -{C1} {proxies1}{A} - {X}[{Z}{er}{X}]       ',end='')
     for i in range(300):
          t = threading.Thread(target=af)
          t.start()
if Get_aobsh in '3':
     print("""
السلام عليكم
وياكم خادمك الصغير
المبرمج عفريتون
الحساب الرسمي ع التلكرام
@AFR_0
القناة الرسمية ع التلكرام
@LPB_B
الادات كل اتصالاتها مسحوبه
من البرنامج الرسمي
لشركة تيكتوك اصدار
33.3.4
الادات تبلغ ب3 انواع اجهزه
اوبو وسامسونك وريلمي فقط
وكل جهاز وله مشتقاته
وتبلغ باكثر من 10 لغات
واكثر من 10 دول
وباكثر من الاف  الايبيات
ويتوفر بها حسابات لهدم الحساب
وتخلل به وللشك بشركه 
انه ينتهك
تابع الخطوات 
لكي تعرف تزيل الحسابات
القويه وضعيفه
@==========================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
لتطيير اي حساب مهم كانت قوته
لازم تتبع الخطوات الي اذكرهن حرفين
تتبعهن خطوه بخطوه تخطاء بخطوه
راح يكون صعب اطير الحساب
@==================================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
الخطوه الاوله
لازم تسحب سيزن ايدي
30 حساب اقل شي
وكل 3 ايام او بلحد الادنا سبوع
لازم تغير الحسابات
وتكدر ترجعلهن السبوع الي بعده
وكذالك تسحب سيزنات جديده
رقم واحد لسحب السيزن داخل الادات
ولازم تسحب فقط من الادات
@================================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
الخطوه الثانيه 
تسحب بروكسي مايقل
عن 500 بروكسي
وبعد استخدامك لسحب البروكسي
فعلم ان البروكسيات انتهن 
وماراح يخدمن بشي 
غير الضرر الك
فلازم تعيد السحب من جديد
@=========================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
الخطوه الثالثه
تقوم بابلاغ ع الحساب فقط من
السيزنات المتوفره داخل الادات
ولازم 
تشوف انو كل السيزنات بلغن ع الحساب
وبهذي الحاله راح تكدر تعيد تشغيل الادات
لان الحساب نهدم جذرين
@========================================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
الخطوه الرابعه
وهنا اول خطوه مهمه الك
لازم تسويه ركز وياي
انته سحبت سيزن ايدي
من 30 حساب
تجي تاخذ من 30 سيزن
20 تخصصهم فقط البدايت
البلاغ الاوليه
هنا انته مجهز بروكسي 500 جديد
وتختار البلاغ كون الي تشوف
الحساب المنتهك بي
وتخلي 20 سيزن
وتخلهم يبلغن
لحد متشوف كل الفيدوهات انضربن
@===============================@
""")
     input("أضغط انتر للتكمله")
     clear()
     print("""
الخطوه الخامسه
وهي ثاني خطوه مهمه
يكون ساحب 500 بروكسي جديد
وبقن 10 سيزنات
من 30 سيزن
وهذا الشي راجعلك تكدر تكثرهن 
المهم يكونن مختلفات مامتشابهات بلي بلغت بيهن
وكذالك تعيد ضرب الحساب بيهن
ويفضل تبلغ بيهن بلاغ اخر
وهذي نسبت 75%
راح يطير عنك الحساب اذا
طبقت الخطوات
وشرح مثل مافهمتك بيهن
وماراح يصعب عليك اي حساب 
انشالله
واذا شفت حساب مابي انتهاكات
وقوي ضاعف السيزنات اكثر راح اجيب ازالته 
100%
""")
if Get_aobsh in '4':
     clear()
     usr=['z1.h4','94qr4',' z1.h4',' 94qr4','z1.h4 ','94qr4 ',"fwd1"]
     g = input( f"       {X}[{F}×{X}]{Z} Target username - يوزر الضحيه  :  "+L)
     clear()
     if g in usr:
          print("هل انت غبي الى هذهي الدرجه لكي تبلغ ع مطور الادات");exit()
     else:
          pass
     try:
          headers = {"user-agent": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.198 Mobile Safari/537.36",}
          r = requests.get(f"https://www.tiktok.com/@{g}", headers=headers).text.split('"userInfo"')[1].split('"statusMsg":"')[0]

          ur=r.split('"secUid":"')[1].split('",')[0]
          id=r.split('"user":{"id":"')[1].split('",')[0]
          nickname=r.split('"nickname":"')[1].split('",')[0]
     except:print("يرجا التاكد من اليوزر");exit()
     clear()
     uid1=[]
     
     print(f"{Z}[{F}1{Z}] {C1}سيزن من الادات")
     print(f"{Z}[{F}2{Z}] {C1}سيزن خاص بيك")
     aobsh=input(f"{X}[{F}×{X}]{Z} اختار : "+L)
     clear()
     if aobsh == '1':
          try:

               h3={'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36',}

               ttwid=requests.head('https://www.tiktok.com/',headers=h3).cookies.get_dict()['ttwid']
          except requests.exceptions.ConnectionError:
               print("يرجا التاكد من النت واعد المحاوله مره اخره");exit()
          except:print("يرجا المحاوله مره اخره");exit()
          
     if aobsh == '2':
          try:
               clear()
               jum = int(input(f' عدد  سيزنات : '+X))
          except ValueError:
               print(Z+'الرجاء كتابت كم  سيزنات بلارقام')
               exit()
          if jum<1 or jum>1000:
               print(Z+'فشل تفريغ  ')
               exit()
          yz = 0
          for met in range(jum):
               yz+=1
               clear()
               kl = input(f'السيزن  '+X+str(yz)+F+' : '+L)
               uid1.append(kl)
          for userr in uid1:
               
               try:
                    rh=requests.get('https://api16-normal-c-useast1a.tiktokv.com/passport/account/info/v2/?',headers={'cookie': f'sessionid={userr};'})
                    if 'success' in str(rh.text):
                         if userr in sisn:
                              pass
                         else:
                              sisn.append(userr)
                    if 'error' in str(rh.text):
                         print('ان هذا السيزن ايدي متوقف')
                         print(userr)
                         time.sleep(5)
               except requests.exceptions.ConnectionError:
                    print(Z+'       الاتصال في النت ظعيف')
     clear()

     if len(sisn)<1 :
          print(Z+'السيزنات اقل من 10 ')
          exit()
     else:
          if aobsh == '2':
               reason1=[]
               print(f"    {X}[{F}1{X}]{C1} العنف والايذاء والاستغلال الاجرامي")
               print(f"    {X}[{F}2{X}]{C1} الكراهيه والتحرش")
               print(f"    {X}[{F}3{X}]{C1} الانتحار وإيذاء النفس")
               print(f"    {X}[{F}4{X}]{C1} اضطرابات الأكل وصورة الجسم غير الصحية")
               print(f"    {X}[{F}5{X}]{C1} الأنشطة والتحديات الخطرة")
               print(f"    {X}[{F}6{X}]{C1} العري والمحتوى الجنسي")
               print(f"    {X}[{F}7{X}]{C1} المحتوى صادم وبشع المنظر")
               print(f"    {X}[{F}8{X}]{C1} معلومات خاطئه")
               print(f"    {X}[{F}9{X}]{C1} السلوك المخادع والغش")
               print(f"    {X}[{F}10{X}]{C1} السلع والانشطة الخاضعه للتنظيم")
               print(f"    {X}[{F}11{X}]{C1} الغش والاحتيال")
               print(f"    {X}[{F}12{X}]{C1} مشاركة المعلومات الشخصية")
               print(f"    {X}[{F}13{X}]{C1} تقليد والملكية الفكرية")
               print(f"    {X}[{F}14{X}]{C1} اخرى")
               xxx=input(f"{X}[{F}×{X}]{Z}   اختار المناسب لك : "+L)
               clear()
               if xxx == '1':
                    print(f"{X}[{F}1{X}]{J22} استغلال الأشخاص الذين تقل أعمارهم عن 18 عامًا أو إساءة معاملتهم")
                    print(f"{X}[{F}2{X}]{J22} العنف الجسدي والتهديدات العنيفة")
                    print(f"{X}[{F}3{X}]{J22} الاستغلال والاعتداء الجنسي")
                    print(f"{X}[{F}4{X}]{J22} الاستغلال البشري")
                    print(f"{X}[{F}5{X}]{J22} الإساءة للحيوان")
                    print(f"{X}[{F}6{X}]{J22} الأنشطة الإجرامية الأخرى")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
                    elif xxx == '3':reason1=('902112')
                    elif xxx == '4':reason1=('902112')
                    elif xxx == '5':reason1=('902112')
                    elif xxx == '6':reason1=('902112')
               elif xxx == '2': 
                    print(f"{X}[{F}1{X}]{J22} الكلام الذي يحض على الكراهية والسلوكيات البغيضة")
                    print(f"{X}[{F}2{X}]{J22} التحرش والتنمر")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
               elif xxx == '3':reason1=('902112')
               elif xxx == '4':reason1=('902112')
               elif xxx == '5':reason1=('902112')
               elif xxx == '6':
                    print(f"{X}[{F}1{X}]{J22} النشاط الجنسي للشباب والاستدراج الجنسي والاستغلال الجنسي")
                    print(f"{X}[{F}2{X}]{J22} السلوك الموحي جنسيًا بواسطة الشباب")
                    print(f"{X}[{F}3{X}]{J22} النشاط الجنسي للبالغين والخدمات الجنسية والاستدراج الجنسي")
                    print(f"{X}[{F}4{X}]{J22} عُري البالغين")
                    print(f"{X}[{F}5{X}]{J22} اللغة الجنسية الفاحشة")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
                    elif xxx == '3':reason1=('902112')
                    elif xxx == '4':reason1=('902112')
                    elif xxx == '5':reason1=('902112')
               elif xxx == '7':reason1=('902112')
               elif xxx == '8':
                    print(f"{X}[{F}1{X}]{J22} معلومات خاطئة عن الانتخابات")
                    print(f"{X}[{F}2{X}]{J22} المعلومات الضارة المضللة")
                    print(f"{X}[{F}3{X}]{J22} التزييف العميق (Deepfakes) الوسائط التي تم التلاعب بها")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
                    elif xxx == '3': reason1=('902112')
               elif xxx == '9':
                    print(f"{X}[{F}1{X}]{J22} التفاعل الزائف")
                    print(f"{X}[{F}2{X}]{J22} مزعج")
                    print(f"{X}[{F}3{X}]{J22} محتوى مرتبط بعلامة تجارية غير معلن عنه")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
                    elif xxx == '3':reason1=('902112')
               elif xxx == '10':
                    print(f"{X}[{F}1{X}]{J22} المقامرة")
                    print(f"{X}[{F}2{X}]{J22} الكحول والتبغ والمخدرات")
                    print(f"{X}[{F}3{X}]{J22} الأسلحة النارية والأسلحة الخطرة")
                    print(f"{X}[{F}4{X}]{J22} تجارة السلع والخدمات الأخرى الخاضعة للرقابة")
                    xxx=input(f"{X}[{F}×{X}]{Z}اختار المناسب لك : "+L)
                    if xxx == '1':reason1=('902112')
                    elif xxx == '2':reason1=('902112')
                    elif xxx == '3':reason1=('902112')
                    elif xxx == '4':reason1=('902112')
               elif xxx == '11':reason1=('902112')
               elif xxx == '12':reason1=('902112')
               elif xxx == '13':reason1=('902112')
               elif xxx == '14':
                    print("لازم تكتبه حسب الانتهاك الي بلحساب")
                    ktab=input("يرجا كتابة النص بلغه الانكليزي : ")
                    
          O = open('SAIPR_REPORT_AFRIT_SAIPR.txt','r').read().splitlines()
          for prox in O:
                    
               ls.append(prox)
          clear()
          def afr(aweme_id,sessionid):
                    global tr,fa,er
                    proxies1=str(random.choice(ls))
                    _rticket = int(time.time() * 1000)
                    ts=str(int(time.time() * 1000))[:10]
                    from uuid import uuid4
                    uid=str(uuid4())
                    install_id = random.randrange(7334285683765348101, 7334285999999999999)
                    device_id=random.randrange(7283928371561793029, 7283929999999999999)
                    openudid = str(binascii.hexlify(os.urandom(8)).decode())
                    tz_name = random.choice(['America/New_York', 'Europe/London', 'Asia/Tokyo', 'Australia/Sydney', 'Asia/Kolkata', 'America/Los_Angeles', 'Europe/Paris', 'Asia/Dubai', 'America/Sao_Paulo', 'Asia/Shanghai'])
                    webcast_language = random.choice(['en', 'es', 'fr', 'de', 'ja', 'pt', 'it', 'ru', 'ar', 'hi'])
                    current_region = random.choice(['US', 'UK', 'CA', 'AU', 'IN', 'BR', 'FR', 'DE', 'IT', 'ES','AB'])
                    region = random.choice(['US', 'UK', 'CA', 'AU', 'IN', 'BR', 'FR', 'DE', 'IT', 'ES'])
                    screen_height = random.randint(600,1080)
                    screen_width = random.randint(800,1920)
                    samsung = ["SM-G975F","SM-G532G","SM-N975F","SM-G988U","SM-G977U","SM-A705FN","SM-A515U1","SM-G955F","SM-A750G","SM-N960F","SM-G960U","SM-J600F","SM-A908B","SM-A705GM","SM-G970U","SM-A307FN","SM-G965U1","SM-A217F","SM-G986B","SM-A207M","SM-A515W","SM-A505G","SM-A315G","SM-A507FN","SM-A505U1","SM-G977T","SM-A025G","SM-J320F","SM-A715W","SM-A908N","SM-A205F","SM-G988B","SM-N986B","SM-A715F","SM-A515F","SM-G965F","SM-G960F","SM-A505F","SM-A207F","SM-A307G","SM-G970F","SM-A107F","SM-G935F","SM-G935A","SM-A310F","SM-J320FN"]
                    oppo =['CPH2359','CPH2457','CPH2349','CPH2145','CPH2293','CPH2343','CPH2127','CPH2197','CPH2173','CPH2371','CPH2269','CPH2005','CPH2185']
                    realme=['RMX3501','RMX3085','RMX1921','RMX3771','RMX3461','RMX3092','RMX3393','RMX3392','RMX1821','RMX1825','RMX3310',]
                    phone=random.choice([samsung,oppo,realme.TECNO .SPARK ])
                    type1=random.choice(phone)
                    if 'SM' in type1 :
                         brand='samsung'
                         dev=type1.split('-')[1]
                    if 'RMX' in type1:
                         brand='realme'
                         dev=type1.split('X')[1]
                    if 'CPH' in type1:
                         brand='OPPO'
                         dev=type1.split('H')[1]
                    if   'TECNO' in type1:
                        TECNO='SPARK 10C'
                    

                    off=int(round((datetime.datetime.now() - datetime.datetime.utcnow()).total_seconds()))
                    if aobsh == '1':
                         time1 = int(datetime.datetime.now().timestamp())
                         sdsd=['902112',]
                         reason=str(random.choice(sdsd))
                         pro1=urlencode({'WebIdLastTime': time1,

                              'aid': '1988',

                              'app_language': webcast_language,

                              'app_name': 'tiktok_web',

                              'aweme_type': '0',

                              'browser_language': webcast_language,

                              'browser_name': 'Mozilla',

                              'browser_online': 'true',

                              'browser_platform': 'Win32',

                              'browser_version': '5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36',

                              'channel': 'tiktok_web',

                              'cookie_enabled': 'true',
                              'device_id': device_id,

                              'device_platform': 'web_pc',

                              'focus_state': 'true',

                              'from_page': 'video',

                              'history_len': '8',

                              'is_fullscreen': 'false',

                              'is_page_visible': 'true',

                              'is_sub_only_video': '0',

                              'lang': webcast_language,

                              'nickname': nickname,

                              'object_id': aweme_id,

                              'object_owner_id': id,

                              'os': 'windows',

                              'owner_id': id,

                              'play_mode': 'browser_mode',

                              'reason': reason,

                              'referer': 'referer',
                              'report_type': 'video',

                              'reporter_id': '6856361445673272326',

                              'screen_height': screen_height,

                              'screen_width': screen_width,

                              'target': aweme_id,

                               'relevant_law':1 ,
                               'report_desc': 2,
                               'report_signature': 3,
                               'root_referer': 'https://www.google.com/',

                              ' legal_jurisdiction': 'be',
                              ' nickname': 'Farouk Wanle',
                               'trusted':'_flagger_email', 

                              'video_id': aweme_id,

                              'video_owner': '[object Object]',

                              'webcast_language': webcast_language,

                              'msToken': 'IV--mbNJVFdJzW3ezHWueGOYzCbGzWsDOhS5NTUcIhaUlI-PaYeT0XEu1G8dbDVs2Sht-5LXELzOfW6634YUJ6iPNP1JnmQPdnuaGBZ-s6BR2wxIzC9QAvsHIQ6PFliZzFjJ9zsarQBdjw==',

                              'msToken': 'w7Dwu7yXuV_QZ2Gln8An6PeXwM6aWAL3ss-a3epdRBhi8Gwz80qUryo9Cdnb4rn14K-p5DzfceXIs4TEkbZMCZufVi9hIizRt6OrSKX3b2hbRHOPRPwtiCfcIpN8dmrToz-kroaOXc9nog==',
                              'X-Bogus': 'DFSzswVLP3RR9kGEtWd7JbJ92U6S',
                             
                              'X-Bogus': 'DFSzswVLk6UANJGEtWp3xbJ92UIX',

                              '_signature': '_02B4Z6wo00001qvYUFwAAIDArHJl-y89yw6r2FTAAMyOac',})

                         url='https://www.tiktok.com/aweme/v2/aweme/feedback/?%s'%(pro1)

                         h={

                              'Cookie': f'ttwid={ttwid}; sid_tt='+sessionid+'; sessionid='+sessionid+'; sessionid_ss='+sessionid+';',

                              'Referer': 'https://www.tiktok.com/@'+g+'/video/'+aweme_id,

                              'Sec-Fetch-Site': 'same-origin',

                              'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36',}
                         
                    #Other
                    if aobsh == '2':
                         if xxx == '14':
                              pro=urlencode({
                              'logout_reporter_email':'',
                              'reason':'9013',
                              'enter_from':'homepage_hot',
                              'owner_id':id,
                              'report_type':'video',
                              'object_id':aweme_id,
                              'no_hw':'1',
                              'submit_type':'1',
                              'isFirst':'1',
                              'trusted_flagger_email':'',
                              'report_signature':f'{names.get_last_name()} {names.get_last_name()} {names.get_last_name()}',
                              'extra_log_params':'%7B%22last_from_group_id%22%3A%22'+aweme_id+'%22%2C%22is_ecom%22%3A%220%22%7D',
                         'report_desc':f'{ktab}',
                              'category':'',
                              'legal_jurisdiction':'dk',
                              'iid':install_id,
                              'device_id':device_id,
                              'ac':'wifi',
                              'channel':'googleplay',
                              'aid':'1233',
                              'app_name':'musical_ly',
                              'version_code':'330304',
                              'version_name':'33.3.4',
                              'device_platform':'android',
                              'os':'android',
                              'ab_version':'33.3.4',
                              'ssmix':'a',
                              'device_type':type1,
                              'device_brand':brand,
                              'language':webcast_language,
                              'os_api':'28',
                              'os_version':'9',
                              'openudid':openudid,
                              'manifest_version_code':'2023303040',
                              'resolution':f'{screen_width}*{screen_height}',
                              'dpi':'191',
                              'update_version_code':'2023303040',
                              '_rticket':_rticket,
                              'is_pad':'0',
                              'current_region':current_region,
                              'app_type':'normal',
                              'sys_region':region,
                              'mcc_mnc':'21890',
                              'timezone_name':tz_name,
                              'residence':current_region,
                              'app_language':webcast_language,
                              'carrier_region':current_region,
                              'ac2':'wifi',
                              'uoo':'0',
                              'op_region':current_region,
                              'timezone_offset':off,
                              'build_number':'33.3.4',
                              'host_abi':'arm64-v8a',
                              'locale':webcast_language,
                              'region':region,
                              'ts':ts,
                              'cdid':uid})
                              
                         #Harassment and bullying
                         else:
                              pro=urlencode({
                              'reason':reason1[0],
                              'enter_from':'homepage_hot',
                              'owner_id':id,
                              'report_type':'video',
                              'object_id':aweme_id,
                              'uri':'',
                              'no_hw':'1',
                              'current_video_play_time':'12',
                              'isFirst':'1',
                              'extra_log_params':'%7B%22last_from_group_id%22%3A%22'+aweme_id+'%22%2C%22is_ecom%22%3A%220%22%7D',
                              'report_desc':'',
                              'category':'',
                              'iid':install_id,
                              'device_id':device_id,
                              'ac':'wifi',
                              'channel':'googleplay',
                              'aid':'1233',
                              'app_name':'musical_ly',
                              'version_code':'330304',
                              'version_name':'33.3.4',
                              'device_platform':'android',
                              'os':'android',
                              'ab_version':'33.3.4',
                              'ssmix':'a',
                              'device_type':type1,
                              'device_brand':brand,
                              'language':webcast_language,
                              'os_api':'28',
                              'os_version':'9',
                              'openudid':openudid,
                              'manifest_version_code':'2023303040',
                              'resolution':f'{screen_width}*{screen_height}',
                              'dpi':'191',
                              'update_version_code':'2023303040',
                              '_rticket':_rticket,
                              'is_pad':'0',
                              'current_region':current_region,
                              'app_type':'normal',
                              'sys_region':region,
                              'mcc_mnc':'21890',
                              'timezone_name':tz_name,
                              'residence':current_region,
                              'app_language':webcast_language,
                              'carrier_region':current_region,
                              'ac2':'wifi',
                              'uoo':'0',
                              'op_region':current_region,
                              'timezone_offset':off,
                              'build_number':'33.3.4',
                              'host_abi':'arm64-v8a',
                              'locale':webcast_language,
                              'region':region,
                              'ts':ts,
                              'cdid':uid})
                         u='https://api22-normal-c-useast1a.tiktokv.com/aweme/v2/aweme/feedback/?'
                         url = u+pro
                         payload = f''
                         signed = ttsign(url.split('?')[1], payload, None).get_value()
                         x_gorgon=signed['x-gorgon']
                         x_khronos=signed['x-khronos']
                         xss=signed['x-ss-req-ticket']
                         
                         h={
                         'Cookie':
                         f'sid_tt={sessionid}; sessionid={sessionid}; sessionid_ss={sessionid};',
                        
                         'User-Agent' :f'com.zhiliaoapp.musically/2023306030 (Linux; U; Android 12; {region}; {type1}; Build/NRD90M.{dev}KSU1AQDC;tt-ok/3.12.13.4-tiktok)',#SM-G955N
     
                         'X-Gorgon':x_gorgon,
                         'X-Khronos':x_khronos,
                         'X-SS-REQ-TICKET':xss,
                    }
                    try:
                         r=requests.get(url,headers=h,proxies={'https': f'socks5://{str(random.choice(ls))}','https': f'socks4://{str(random.choice(ls))}','https': f'http://{str(random.choice(ls))}'}).text
                         tr+=1
                         if aweme_id in soso:
                              pass
                         else:
                              soso.append(aweme_id)
                         if sessionid in loop:
                              pass
                         else:
                              loop.append(sessionid)
                         bi = random.choice([F,J,Z,C,B,L,J1,J2,J21,J22,F1,C1,P1])
                         print(bi+f"\r {len(soso)}/{len(tar)} True :{F}[{tr}] {bi}Net :{Z}[{fa}]{bi} {len(loop)}/{len(sisn)}",end=" ");sys.stdout.flush()
                    except:
                         fa +=1
                         bi = random.choice([F,J,Z,C,B,L,J1,J2,J21,J22,F1,C1,P1])
                         print(bi+f"\r {len(soso)}/{len(tar)} True :{F}[{tr}] {bi}Net :{Z}[{fa}]{bi} {len(loop)}/{len(sisn)}",end=" ");sys.stdout.flush()
          
          hussain=0
          while (hussain < len(sisn)):
               for i in sisn :
                    sessionid = str(i.strip())
                    video_list = []
                    max_cursor=0
                    while 1:
                         openudid = str(binascii.hexlify(os.urandom(8)).decode())
                         _rticket = int(time.time() * 1000)
                         ts=str(int(time.time() * 1000))[:10]
                         u=f'https://api2-19-h2.musical.ly/aweme/v1/aweme/post/?source=0&max_cursor={max_cursor}&sec_user_id={ur}&count=20&app_skin=white&manifest_version_code=2021600040&_rticket={_rticket}&app_language=en&app_type=normal&iid=7368148584393508613&channel=googleplay&device_type=SM-G973N&language=en&cpu_support64=true&host_abi=armeabi-v7a&locale=en&uuid=354730022862944&resolution=720*1280&openudid={openudid}&update_version_code=2021600040&ac2=wifi5g&sys_region=US&os_api=32&uoo=0&timezone_name=Africa%2FNairobi&dpi=240&carrier_region=IQ&ac=wifi&device_id=6980700221262235138&pass-route=1&mcc_mnc=31002&os_version=12&timezone_offset=10800&version_code=160004&carrier_region_v2=310&app_name=musical_ly&ab_version=16.0.4&version_name=16.0.4&device_brand=samsung&op_region=IQ&ssmix=a&pass-region=1&device_platform=android&build_number=16.0.4&region=US&aid=1233&ts={ts}'
                         signed = ttsign(u.split('?')[1], "", None).get_value()
                         x_gorgon=signed['x-gorgon']
                         x_khronos=signed['x-khronos']
                         h={'Accept-Encoding': 'gzip', 
                         'Connection': 'Keep-Alive', 
                         'Cookie': f'sessionid={random.choice(["58722b392919a8cb490e9150a0214e9d","7102eb970e667d3e870a53eaa9b72dcd","4c1b5e5553effcceab87f5def506bd39","f448b52989da0e9186516af7d6618018","fdd47427291edd263755a5e1f8f57561","94ec15f73dd664ff5f27195bb3c4f2e4","1eb64c7737a9ff4bd73ba79f865fa216",])}', 
                         'Host': 'api2-19-h2.musical.ly', 
                         'sdk-version': '1', 'User-Agent': 'okhttp/3.10.0.1', 
                         'X-Gorgon': x_gorgon, 
                         'X-Khronos': x_khronos}
                         try:
                            r=requests.get(u,headers=h).json()
                        
                            try:
                                max_cursor = r["max_cursor"]
                            except Exception:
                                if "No more videos" in requests.get(u,headers=h).text:
                                    break
                            aweme_list = r["aweme_list"]
                            for aweme in aweme_list:
                                aweme_id = aweme["aweme_id"]
                                if aweme_id in tar:
                                    pass
                                else:
                                    tar.append(aweme_id)
                                threading.Thread(
                                    target=afr,
                                    args=(
                                        aweme_id,
                                        sessionid,
                                    ),
                                ).start()
                         
                         except:pass
                    
    

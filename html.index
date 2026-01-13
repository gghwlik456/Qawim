import requests, re, base64, uuid, string, random, time
from itertools import product

# -------- تسجيل الدخول --------
def login(user, password):
    rd = ''.join(random.choices(string.ascii_lowercase + string.digits, k=16))
    my_uuid = str(uuid.uuid4())
    modified_uuid = my_uuid[:8] + "should_trigger_override_login_success_action" + my_uuid[8:]

    data = {
        "params": "{\"client_input_params\":{\"contact_point\":\"" + user + "\",\"password\":\"#PWD_INSTAGRAM:0:0:" + password + "\",\"device_id\":\"android-" + rd + "\",\"event_step\":\"home_page\"},\"server_params\":{\"device_id\":\"android-" + rd + "\",\"waterfall_id\":\"" + modified_uuid + "\"}}"
    }
    headers = {
        "User-Agent": "Instagram 303.0.0.0.59 Android",
        "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",
        "X-Ig-App-Id": "567067343352427"
    }

    r = requests.post("https://i.instagram.com/api/v1/bloks/apps/com.bloks.www.bloks.caa.login.async.send_login_request/", headers=headers, data=data)
    if "Bearer" in r.text:
        session = re.search(r'Bearer IGT:2:(.*?),', r.text).group(1).strip()
        session = session[:-8]
        decoded = base64.b64decode(session).decode('utf-8')
        sessionid = re.search(r'"sessionid":"(.*?)"}', decoded).group(1)
        print(f"[ + ] Logged in as @{user}")
        return sessionid
    else:
        print("[ - ] Failed to login")
        exit()

# -------- تغيير الاسم --------
def change_username(sessionid, new_username):
    headers = {
        "User-Agent": "Instagram 303.0.0.0.59 Android",
        "Cookie": f"sessionid={sessionid}",
        "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8"
    }

    data = {
        "username": new_username
    }

    response = requests.post("https://i.instagram.com/api/v1/accounts/set_username/", headers=headers, data=data)
    if response.status_code == 200 and f'"username":"{new_username}"' in response.text:
        print(f"[ ✅ ] Username changed successfully to: {new_username}")
        return True
    else:
        if "username isn't available" in response.text:
            print(f"[ ❌ ] {new_username} is taken.")
        elif "feedback_required" in response.text:
            print(f"[ 🚫 ] Rate limited or blocked temporarily. Try again later.")
            exit()
        else:
            print(f"[ ❌ ] Failed to change username to: {new_username}")
        return False

# -------- توليد الأسماء الثنائية --------
def generate_usernames():
    chars = string.ascii_lowercase + string.digits
    usernames = [''.join(i) for i in product(chars, repeat=2)]
    random.shuffle(usernames)
    return usernames

# -------- Main --------
if __name__ == "__main__":
    USER = input("[ + ] Username: ")
    PASS = input("[ + ] Password: ")

    sessionid = login(USER, PASS)
    names = generate_usernames()

    print(f"[ * ] Trying {len(names)} usernames...\n")

    for name in names:
        success = change_username(sessionid, name)
        if success:
            break
        time.sleep(2)  # تأخير 2 ثانية بين كل محاولة

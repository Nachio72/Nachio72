from BotAmino import BotAmino

print("wait...")
client = BotAmino()
client.prefix = "/"  # set the prefix to /
client.wait = 10  # wait 10 sec before doing a new command


def test(data):
    return data.authorId == ["your_user_id"]



@client.command("ping", test) # "ping" the command and test the function, if test is True the command will be executed, else it will not
def ping(data):
    data.subClient.send_message(data.chatId, message="pong!")


@client.command("pong") # "pong" the command, the test function is not necessary
def ping(data):
    if data.subClient.is_in_staff(data.authorId): # will execute the command if the user is in the amino's staff (learder/curator)
        data.subClient.send_message(data.chatId, message="ping!")


@client.answer("hey")
def hello(data):
    data.subClient.send_message(data.chatId, message="Hey! Hey!")


@client.on_member_join_chat()
def say_hello(data):
    data.subClient.send_message(data.chatId, f"welcome here {data.author}!")


@client.on_member_leave_chat(["chatId"]) # the chatId is not necessary, put one if you want a specified chat only
def say_goodbye(data):
    data.subClient.send_message(data.chatId, f"See you soon {data.author}!")



client.launch()
print("ready")

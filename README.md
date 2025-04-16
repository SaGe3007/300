import asyncio
import logging
from aiogram import Bot, Dispatcher, F, types
from aiogram.filters import Command
from aiogram.types import WebAppInfo

logging.basicConfig(level=logging.INFO)

API_TOKEN = '7652584013:AAGSJ5naF4qnVDx0geNzgR6q0ExzjFCgSic'
bot = Bot(token=API_TOKEN)
dp = Dispatcher()

main_menu = types.ReplyKeyboardMarkup(
    keyboard=[
        [
            types.KeyboardButton(text="Связаться со специалистом"),
            types.KeyboardButton(
                text="Рассчитать стоимость доставки груза",
                web_app=WebAppInfo(url="https://sage3007.github.io/ctc-webapp.io/")
            )
        ]
    ],
    resize_keyboard=True
)

@dp.message(Command("start"))
async def send_welcome(message: types.Message):
    await message.answer(
        "Здравствуйте! Я бот call-центра «Центральной Транспортной Компании».\n\n"
        "Наша компания постоянно растет и развивается, расширяя спектр своих возможностей, "
        "повышая качество сервиса оказываемых услуг и географию перевозок.\n\n"
        "Наши услуги:\n"
        "🔹 Доставка грузов из ЕС, США, Китая в страны СНГ\n"
        "🔹 Перевозка автомобилей и спец. техники\n"
        "🔹 Мультимодальные перевозки\n"
        "🔹 Контейнерные перевозки\n"
        "🔹 Таможенное оформление\n"
        "🔹 Проведение платежей Вашему поставщику в Европу и Китай",
        reply_markup=main_menu
    )

@dp.message(F.text == "Связаться со специалистом")
async def contact_specialist(message: types.Message):
    await message.answer("Если у Вас есть вопросы напишите специалисту :\n" 
    "Telegram — @centrtranscompany\n"
    "WhatsApp — https://wa.me/375295579068 ",  disable_web_page_preview=True )

async def main():
    try:
        await dp.start_polling(bot)
    finally:
        await bot.session.close()

if __name__ == "__main__":
    asyncio.run(main())

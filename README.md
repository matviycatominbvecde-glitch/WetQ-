import React, { useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Input } from "@/components/ui/input"; import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"; import { motion } from "framer-motion"; import { Plane } from "lucide-react";

export default function WetQWebsite() { const [registered, setRegistered] = useState(false); const [balance] = useState("∞"); const [from, setFrom] = useState(""); const [to, setTo] = useState(""); const [flightClass, setFlightClass] = useState(""); const [flightType, setFlightType] = useState(""); const [username, setUsername] = useState(""); const [tickets, setTickets] = useState([]);

const buyTicket = () => { if (!from || !to || !flightClass || !flightType) { alert("Заповніть всі поля ✈️"); return; }

const newTicket = {
  id: Date.now(),
  from,
  to,
  flightClass,
  flightType,
};

setTickets([...tickets, newTicket]);

};

const citiesEurope = [ "Париж", "Берлін", "Рим", "Мадрид", "Прага", "Варшава", "Відень", "Будапешт" ];

const citiesAsia = [ "Токіо", "Сеул", "Бангкок", "Сінгапур", "Пекін", "Дубай", "Стамбул", "Куала-Лумпур" ];

const allCities = [...citiesEurope, ...citiesAsia];

return ( <div className="min-h-screen bg-gradient-to-br from-blue-100 to-purple-200 p-6 grid gap-6"> <motion.h1 initial={{ opacity: 0, y: -20 }} animate={{ opacity: 1, y: 0 }} className="text-4xl font-bold text-center flex items-center justify-center gap-2" > WetQ ♥️ Airlines <Plane /> </motion.h1>

{/* Реєстрація */}
  <Card className="rounded-2xl shadow-xl p-4">
    <CardContent className="space-y-4">
      <h2 className="text-xl font-semibold">Реєстрація</h2>
      {!registered ? (
        <div className="space-y-2">
          <Input
            placeholder="Ім'я"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
          />
          <Input placeholder="Email" />
          <Button onClick={() => setRegistered(true)}>
            Зареєструватися
          </Button>
        </div>
      ) : (
        <div className="text-green-600 space-y-1">
          <p>✅ Вітаємо, {username}!</p>
          <p>Баланс: {balance} WQ Coins</p>
        </div>
      )}
    </CardContent>
  </Card>

  {/* Бронювання */}
  <Card className="rounded-2xl shadow-xl p-4">
    <CardContent className="space-y-4">
      <h2 className="text-xl font-semibold">Бронювання квитка</h2>

      <Select onValueChange={setFrom}>
        <SelectTrigger>
          <SelectValue placeholder="Звідки" />
        </SelectTrigger>
        <SelectContent>
          {allCities.map((city) => (
            <SelectItem key={city} value={city}>
              {city}
            </SelectItem>
          ))}
        </SelectContent>
      </Select>

      <Select onValueChange={setTo}>
        <SelectTrigger>
          <SelectValue placeholder="Куди" />
        </SelectTrigger>
        <SelectContent>
          {allCities.map((city) => (
            <SelectItem key={city} value={city}>
              {city}
            </SelectItem>
          ))}
        </SelectContent>
      </Select>

      <Select onValueChange={setFlightClass}>
        <SelectTrigger>
          <SelectValue placeholder="Клас" />
        </SelectTrigger>
        <SelectContent>
          <SelectItem value="Економ">Економ</SelectItem>
          <SelectItem value="Бізнес">Бізнес</SelectItem>
          <SelectItem value="Перший">Перший клас</SelectItem>
          <SelectItem value="VIP">VIP</SelectItem>
        </SelectContent>
      </Select>

      <Select onValueChange={setFlightType}>
        <SelectTrigger>
          <SelectValue placeholder="Тип польоту" />
        </SelectTrigger>
        <SelectContent>
          <SelectItem value="В один бік">В один бік</SelectItem>
          <SelectItem value="Туди й назад">Туди й назад</SelectItem>
          <SelectItem value="Приватний рейс">Приватний рейс</SelectItem>
        </SelectContent>
      </Select>

      <Button onClick={buyTicket}>Купити квиток</Button>
    </CardContent>
  </Card>

  {/* Мої квитки */}
  <Card className="rounded-2xl shadow-xl p-4">
    <CardContent>
      <h2 className="text-xl font-semibold">Мої квитки</h2>
      {tickets.length === 0 ? (
        <p>У вас ще немає квитків.</p>
      ) : (
        <div className="grid gap-3 mt-3">
          {tickets.map((ticket) => (
            <motion.div
              key={ticket.id}
              initial={{ opacity: 0, x: -20 }}
              animate={{ opacity: 1, x: 0 }}
              className="p-3 bg-white rounded-2xl shadow"
            >
              ✈️ {ticket.from} → {ticket.to} | {ticket.flightClass} | {ticket.flightType}
            </motion.div>
          ))}
        </div>
      )}
    </CardContent>
  </Card>

  {/* Інтерактивна карта (імітація) */}
  <Card className="rounded-2xl shadow-xl p-4">
    <CardContent className="space-y-2">
      <h2 className="text-xl font-semibold">Карта напрямків</h2>
      <div className="h-48 bg-blue-50 rounded-2xl flex items-center justify-center text-center p-4">
        🌍 Натисніть місто у списку, щоб обрати напрямок.
        <br />
        (Тут можна підключити реальну карту Google Maps або Leaflet)
      </div>
    </CardContent>
  </Card>

  {/* Анімація літака */}
  <motion.div
    animate={{ x: [0, 300, 0] }}
    transition={{ repeat: Infinity, duration: 6 }}
    className="text-3xl text-center"
  >
    🛫
  </motion.div>
</div>

); }

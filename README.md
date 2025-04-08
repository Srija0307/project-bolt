<!doctype html>

<html lang="en">

  <head>

    <meta charset="UTF-8" />

    <link rel="icon" type="image/svg+xml" href="/vite.svg" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <title>Vite + React + TS</title>

    <script type="module" crossorigin src="/assets/index-o3K_9hlM.js"></script>

    <link rel="stylesheet" crossorigin href="/assets/index-BXsrW2bt.css">

  </head>

  <body>

    <div id="root"></div>

  </body>

</html>

import React from 'react';



interface StationSelectorProps {

  value: string;

  onChange: (e: React.ChangeEvent<HTMLSelectElement>) => void;

}



const stations = [

  'Chatrapathi Shivaji Maharaj Terminus',

  'Chennai Central Railway Station',

  'Ahmedabad Junction',

  'Vijayawada Junction',

  'Secunderabad Station'

];



function StationSelector({ value, onChange }: StationSelectorProps) {

  return (

    <div className="space-y-2">

      <label htmlFor="station" className="block text-sm font-medium text-gray-700">

        Select Railway Station

      </label>

      <select

        id="station"

        value={value}

        onChange={onChange}

        className="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 p-2 border"

      >

        <option value="">Select a station</option>

        {stations.map((station) => (

          <option key={station} value={station}>

            {station}

          </option>

        ))}

      </select>

    </div>

  );

}



export default StationSelector;

import React, { useState } from 'react';

import { MapPin, Volume2, AlertTriangle, Bell, Ticket } from 'lucide-react';



const locations = [

  'Public Restroom (Free)',

  'Public Waiting Hall',

  'Waiting Lounge',

  'Cafe',

  'Food Court',

  'Drinking Water',

  'Vending Machine'

];



const getRouteImage = (from: string, to: string) => {

  const routeImages: Record<string, string> = {

};



  const routeKey = `${from}_${to}`;

  return routeImages[routeKey] ||

};



const getCustomDirections = (from: string, to: string) => {

  const directions: Record<string, string> = {

};



  const routeKey = `${from}_${to}`;

  return directions[routeKey] || `Starting from ${from}, walk straight for 50 meters, turn right at the main concourse, continue for 30 meters to reach ${to}.`;

};



const alerts = [

  {

    type: 'urgent',

    message: 'Platform 3 under maintenance. Please use alternative routes.',

    timestamp: '10 mins ago'

  },

  {

    type: 'info',

    message: 'New food stall opened near Platform 2 waiting area',

    timestamp: '1 hour ago'

  },

  {

    type: 'warning',

    message: 'Elevator near Platform 1 temporarily out of service',

    timestamp: '2 hours ago'

  }

];



const ticketCounters = [

  { id: 1, status: 'Open', waitTime: '5-10 mins', type: 'General' },

  { id: 2, status: 'Open', waitTime: '15-20 mins', type: 'Senior Citizen/Disabled' },

  { id: 3, status: 'Closed', waitTime: '-', type: 'Premium' },

];



function NavigationPage() {

  const [fromLocation, setFromLocation] = useState('');

  const [toLocation, setToLocation] = useState('');

  

  const handleVoiceGuidance = () => {

    if ('speechSynthesis' in window) {

      const utterance = new SpeechSynthesisUtterance(getCustomDirections(fromLocation, toLocation));

      window.speechSynthesis.speak(utterance);

    }

  };



  const layoutImage = getRouteImage(fromLocation, toLocation);



  return (

    <div className="min-h-screen bg-slate-50">

      <header className="bg-blue-700 text-white py-4 shadow-lg">

        <div className="container mx-auto px-4">

          <h1 className="text-2xl font-bold">Secunderabad Station</h1>

        </div>

      </header>



      <main className="container mx-auto px-4 py-8">

        <div className="grid grid-cols-1 lg:grid-cols-12 gap-8">

          {/* Left Column - Controls */}

          <div className="lg:col-span-4 space-y-6">

            <div className="bg-white p-6 rounded-lg shadow-md space-y-6">

              {/* Location Controls */}

              <div className="space-y-4">

                <div>

                  <label className="block text-sm font-medium text-gray-700 mb-1">

                    Current Location

                  </label>

                  <select

                    value={fromLocation}

                    onChange={(e) => setFromLocation(e.target.value)}

                    className="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 p-2 border"

                  >

                    <option value="">Select your location</option>

                    {locations.map((loc) => (

                      <option key={loc} value={loc}>{loc}</option>

                    ))}

                  </select>

                </div>



                <div>

                  <label className="block text-sm font-medium text-gray-700 mb-1">

                    Destination

                  </label>

                  <select

                    value={toLocation}

                    onChange={(e) => setToLocation(e.target.value)}

                    className="block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500 p-2 border"

                  >

                    <option value="">Select your destination</option>

                    {locations.filter(loc => loc !== fromLocation).map((loc) => (

                      <option key={loc} value={loc}>{loc}</option>

                    ))}

                  </select>

                </div>

              </div>



              {/* Ticket Counter Status */}

              <div className="border-t pt-6">

                <div className="flex items-center gap-2 mb-4">

                  <Ticket className="h-5 w-5 text-blue-600" />

                  <h3 className="font-semibold">Ticket Counter Status</h3>

                </div>

                <div className="space-y-3">

                  {ticketCounters.map((counter) => (

                    <div key={counter.id} className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">

                      <div>

                        <p className="font-medium">Counter {counter.id}</p>

                        <p className="text-sm text-gray-600">{counter.type}</p>

                      </div>

                      <div className="text-right">

                        <p className={`font-medium ${counter.status === 'Open' ? 'text-green-600' : 'text-red-600'}`}>

                          {counter.status}

                        </p>

                        <p className="text-sm text-gray-600">Wait: {counter.waitTime}</p>

                      </div>

                    </div>

                  ))}

                </div>

              </div>

            </div>



            {fromLocation && toLocation && (

              <div className="bg-white p-6 rounded-lg shadow-md">

                <h3 className="font-semibold mb-3 flex items-center gap-2">

                  <MapPin className="h-5 w-5 text-blue-600"  />

                  Directions

                </h3>

                <p className="text-gray-600 mb-4">{getCustomDirections(fromLocation, toLocation)}</p>

                <button

                  onClick={handleVoiceGuidance}

                  className="flex items-center gap-2 bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700 transition-colors w-full justify-center"

                >

                  <Volume2 className="h-5 w-5" />

                  Voice Guidance

                </button>

              </div>

            )}

          </div>



          {/* Right Column - Map and Alerts */}

          <div className="lg:col-span-8 space-y-6">

            <div className="bg-white p-6 rounded-lg shadow-md">

              <div className="relative aspect-[16/9] overflow-hidden rounded-lg">

                <img

                  src={layoutImage}

                  alt={`Route from ${fromLocation} to ${toLocation}`}

                  className="w-full h-full object-cover transition-opacity duration-300"

                />

              </div>

              <p className="text-sm text-gray-500 mt-3">

                {fromLocation && toLocation 

                  ? `Route: ${fromLocation} → ${toLocation}`

                  : "Station Layout Map"}

              </p>

            </div>



            <div className="bg-white p-6 rounded-lg shadow-md">

              <div className="flex items-center gap-2 mb-4">

                <Bell className="h-5 w-5 text-blue-600" />

                <h3 className="font-semibold">Railway Alerts</h3>

              </div>

              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">

                {alerts.map((alert, index) => (

                  <div 

                    key={index} 

                    className={`p-4 rounded-lg flex items-start gap-3 ${

                      alert.type === 'urgent' 

                        ? 'bg-red-50 text-red-700' 

                        : alert.type === 'warning'

                        ? 'bg-yellow-50 text-yellow-700'

                        : 'bg-blue-50 text-blue-700'

                    }`}

                  >

                    <AlertTriangle className="h-5 w-5 flex-shrink-0 mt-0.5" />

                    <div className="flex-1">

                      <p className="text-sm font-medium">{alert.message}</p>

                      <p className="text-xs opacity-75 mt-1">{alert.timestamp}</p>

                    </div>

                  </div>

                ))}

              </div>

            </div>

          </div>

        </div>

      </main>

    </div>

  );

}

export default NavigationPage;



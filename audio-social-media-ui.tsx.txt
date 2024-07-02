import React, { useState } from 'react';
import { MessageCircle, Home, User, Music, Settings, Send, Mic } from 'lucide-react';

const App = () => {
  const [messages, setMessages] = useState([
    { id: 1, user: 'User 1', avatar: '/api/placeholder/40/40', message: "Hey, what's up", isOnline: true },
    { id: 2, user: 'User 2', avatar: '/api/placeholder/40/40', message: "Not much, you?", isOnline: false },
    { id: 3, user: 'User 3', avatar: '/api/placeholder/40/40', message: "Hey there!", isOnline: true },
    { id: 4, user: 'User 4', avatar: '/api/placeholder/40/40', message: "Hello!", isOnline: false },
  ]);

  const [activeChat, setActiveChat] = useState({
    user: 'User 1',
    avatar: '/api/placeholder/40/40',
    messages: [
      { id: 1, text: "Hey there! How's it going?", sent: false },
      { id: 2, text: "Not bad, just working on some code. You?", sent: true },
      { id: 3, text: "Same here! Working on a new project.", sent: false },
    ]
  });

  return (
    <div className="flex h-screen bg-gray-900 text-white">
      {/* Left Sidebar */}
      <div className="w-16 bg-gray-800 flex flex-col items-center py-4">
        <div className="w-10 h-10 bg-purple-600 rounded-full mb-8"></div>
        <SidebarIcon icon={<Home />} />
        <SidebarIcon icon={<User />} />
        <SidebarIcon icon={<MessageCircle />} active />
        <SidebarIcon icon={<Music />} />
        <SidebarIcon icon={<Settings />} />
      </div>

      {/* Messages List */}
      <div className="w-64 bg-gray-800 overflow-y-auto">
        <h2 className="text-xl font-bold p-4">Messages</h2>
        <div className="px-2">
          {messages.map(msg => (
            <MessageItem key={msg.id} {...msg} />
          ))}
        </div>
      </div>

      {/* Chat Window */}
      <div className="flex-1 flex flex-col">
        <div className="flex-1 overflow-y-auto px-4 py-2">
          {activeChat.messages.map(msg => (
            <ChatMessage key={msg.id} {...msg} />
          ))}
        </div>
        <div className="p-4">
          <div className="flex items-center bg-gray-700 rounded-full p-2">
            <input
              type="text"
              placeholder="Type a message..."
              className="flex-1 bg-transparent outline-none"
            />
            <button className="mx-2">
              <Mic size={20} />
            </button>
            <button className="bg-blue-500 rounded-full p-2">
              <Send size={20} />
            </button>
          </div>
        </div>
      </div>

      {/* Right Sidebar */}
      <div className="w-16 bg-gray-800 flex flex-col items-center py-4">
        <UserIcon />
        <UserIcon />
        <UserIcon />
        <UserIcon />
        <UserIcon />
        <UserIcon />
      </div>
    </div>
  );
};

const SidebarIcon = ({ icon, active }) => (
  <div className={`w-10 h-10 flex items-center justify-center rounded-lg mb-4 ${active ? 'bg-gray-700' : 'hover:bg-gray-700'}`}>
    {icon}
  </div>
);

const MessageItem = ({ user, avatar, message, isOnline }) => (
  <div className="flex items-center mb-4">
    <div className="relative">
      <img src={avatar} alt={user} className="w-10 h-10 rounded-full" />
      {isOnline && (
        <div className="absolute bottom-0 right-0 w-3 h-3 bg-green-500 rounded-full border-2 border-gray-800"></div>
      )}
    </div>
    <div className="ml-3">
      <h3 className="font-semibold">{user}</h3>
      <p className="text-sm text-gray-400">{message}</p>
    </div>
  </div>
);

const ChatMessage = ({ text, sent }) => (
  <div className={`max-w-xs ${sent ? 'ml-auto' : ''} mb-2`}>
    <div className={`p-2 rounded-lg ${sent ? 'bg-blue-600' : 'bg-gray-700'}`}>
      {text}
    </div>
  </div>
);

const UserIcon = () => (
  <div className="w-10 h-10 bg-gray-600 rounded-full mb-4"></div>
);

export default App;

<template>
  <div id="app" class="flex justify-start items-start text-gray-500 h-screen">
    <div id="servers" class="bg-gray-900 flex flex-col px-2 py-5 h-screen">
      <ul class="space-y-2">
        <li
          v-for="(server, index) in servers"
          :key="index"
          class="flex justify-center items-center p-0.5 rounded-full hover:rounded-lg bg-gray-700 h-12 w-12 overflow-hidden text-gray-100 text-xl font-semibold tracking-tight"
        >
          {{ initials(server.name) }}
        </li>
      </ul>
    </div>
    <div
      id="chatList"
      class="bg-gray-800 flex flex-col min-w-max h-screen overflow-hidden relative"
    >
      <section id="search" class="py-3 mx-2 border-b border-gray-900">
        <input
          type="text"
          placeholder="Find or start a conversation"
          class="bg-gray-700 px-2 py-2 rounded-md text-sm placeholder-gray-400 w-full"
        />
      </section>
      <div class="link-list overflow-y-scroll h-full">
        <section id="links" class="my-5 mx-2">
          <ul>
            <li
              class="flex justify-start items-center space-x-3 px-3 py-2 text-gray-500 hover:text-gray-100 hover:bg-gray-700 rounded-lg"
            >
              <span>
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"
                  ></path>
                </svg>
              </span>
              <span> Friends </span>
            </li>
            <li
              class="flex justify-start items-center space-x-3 px-3 py-2 text-gray-500 hover:text-gray-100 hover:bg-gray-700 rounded-lg"
            >
              <span>
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"
                  ></path>
                </svg>
              </span>
              <span>Nitro</span>
            </li>
          </ul>
        </section>
        <section id="messages" class="px-2">
          <div id="header" class="flex justify-between items-center">
            <h3
              class="text-xs px-4 py-1 uppercase font-medium hover:text-gray-100"
            >
              Direct Messages
            </h3>
            <span class="pr-2 cursor-pointer text-gray-100">
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M12 6v6m0 0v6m0-6h6m-6 0H6"
                ></path>
              </svg>
            </span>
          </div>
          <div id="messageList" class=" ">
            <ul class="space-y-2">
              <li
                v-for="dm in notDeletedDms"
                :key="dm.id"
                class="list flex justify-start items-center space-x-3 px-2 py-1 hover:bg-gray-900 hover:bg-opacity-20 hover:text-gray-300 rounded-lg cursor-pointer"
              >
                <figure class="flex-shrink">
                  <img
                    class="rounded-full w-8 bg-gray-900 bg-opacity-30"
                    :src="dm.avatar"
                    alt=""
                  />
                </figure>
                <div class="flex-grow">{{ dm.name }}</div>
                <span
                  @click="deleteDm(dm.id)"
                  class="appearOnHover text-gray-500 hover:text-gray-200"
                >
                  <svg
                    class="w-5 h-5"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M6 18L18 6M6 6l12 12"
                    ></path>
                  </svg>
                </span>
              </li>
            </ul>
          </div>
        </section>
      </div>
      <div
        id="aim"
        class="bg-gray-700 flex justify-between items-center p-1.5 text-white"
      >
        <section
          id="user"
          class="flex justify-start items-center space-x-2 w-96"
        >
          <figure class="relative">
            <img
              class="w-12 rounded-full bg-indigo-50"
              src="https://robohash.org/sitmaximedicta.png?size=96x96&set=set1"
              alt=""
            />
            <p
              class="absolute p-0.5 -bottom-0.5 -right-0.5 bg-gray-800 rounded-full"
            >
              <span class="block bg-green-500 p-1.5 rounded-full"></span>
            </p>
          </figure>
          <p data-tooltip="Copy" class="pseudo-bg-green">
            <span class="font-medium">Hasan</span>
            <span class="block text-sm text-gray-400">#889</span>
          </p>
        </section>
        <section id="actions">
          <ul class="flex justify-end items-center">
            <li
              class="p-2 text-gray-400 hover:text-gray-50 hover:bg-gray-700 rounded-lg cursor-pointer"
              data-tooltip="Mute"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 hover:text-gray-200"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M7 4a3 3 0 016 0v4a3 3 0 11-6 0V4zm4 10.93A7.001 7.001 0 0017 8a1 1 0 10-2 0A5 5 0 015 8a1 1 0 00-2 0 7.001 7.001 0 006 6.93V17H6a1 1 0 100 2h8a1 1 0 100-2h-3v-2.07z"
                  clip-rule="evenodd"
                />
              </svg>
            </li>
            <li
              class="p-2 text-gray-400 hover:text-gray-50 hover:bg-gray-700 rounded-lg cursor-pointer"
              data-tooltip="Deafen"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M9.383 3.076A1 1 0 0110 4v12a1 1 0 01-1.707.707L4.586 13H2a1 1 0 01-1-1V8a1 1 0 011-1h2.586l3.707-3.707a1 1 0 011.09-.217zM14.657 2.929a1 1 0 011.414 0A9.972 9.972 0 0119 10a9.972 9.972 0 01-2.929 7.071 1 1 0 01-1.414-1.414A7.971 7.971 0 0017 10c0-2.21-.894-4.208-2.343-5.657a1 1 0 010-1.414zm-2.829 2.828a1 1 0 011.415 0A5.983 5.983 0 0115 10a5.984 5.984 0 01-1.757 4.243 1 1 0 01-1.415-1.415A3.984 3.984 0 0013 10a3.983 3.983 0 00-1.172-2.828 1 1 0 010-1.415z"
                  clip-rule="evenodd"
                />
              </svg>
            </li>
            <li
              class="p-2 text-gray-400 hover:text-gray-50 hover:bg-gray-700 rounded-lg cursor-pointer"
              data-tooltip="User settings"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M11.49 3.17c-.38-1.56-2.6-1.56-2.98 0a1.532 1.532 0 01-2.286.948c-1.372-.836-2.942.734-2.106 2.106.54.886.061 2.042-.947 2.287-1.561.379-1.561 2.6 0 2.978a1.532 1.532 0 01.947 2.287c-.836 1.372.734 2.942 2.106 2.106a1.532 1.532 0 012.287.947c.379 1.561 2.6 1.561 2.978 0a1.533 1.533 0 012.287-.947c1.372.836 2.942-.734 2.106-2.106a1.533 1.533 0 01.947-2.287c1.561-.379 1.561-2.6 0-2.978a1.532 1.532 0 01-.947-2.287c.836-1.372-.734-2.942-2.106-2.106a1.532 1.532 0 01-2.287-.947zM10 13a3 3 0 100-6 3 3 0 000 6z"
                  clip-rule="evenodd"
                />
              </svg>
            </li>
          </ul>
        </section>
      </div>
    </div>
    <main
      class="flex-grow flex flex-col justify-start h-screen bg-gray-600 relative z-0"
    >
      <header
        class="bg-gray-700 border-b border-gray-900 w-full px-2 py-3 flex justify-between items-center"
      >
        <h2 class="atIcon text-gray-50 font-medium">
          Hanh Ngo
          <i class="inline-block mx-1 w-3 h-3 bg-green-500 rounded-full"></i>
        </h2>
        <section
          id="right"
          class="flex justify-end items-center space-x-3 text-gray-300"
        >
          <span class="">
            <svg
              class="w-6 h-6"
              viewBox="0 0 24 24"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M12 11C13.1046 11 14 10.1046 14 9C14 7.89543 13.1046 7 12 7C10.8954 7 10 7.89543 10 9C10 10.1046 10.8954 11 12 11Z"
                fill="currentColor"
              />
              <path
                fill-rule="evenodd"
                clip-rule="evenodd"
                d="M18 9C18 11.973 15.8377 14.441 13 14.917V20C13 20.5523 12.5523 21 12 21C11.4477 21 11 20.5523 11 20V14.917C8.16229 14.441 6 11.973 6 9C6 5.68629 8.68629 3 12 3C15.3137 3 18 5.68629 18 9ZM12 13C14.2091 13 16 11.2091 16 9C16 6.79086 14.2091 5 12 5C9.79086 5 8 6.79086 8 9C8 11.2091 9.79086 13 12 13Z"
                fill="currentColor"
              />
            </svg>
          </span>
          <span class="text-gray-100">
            <svg
              class="w-6 h-6"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M18 9v3m0 0v3m0-3h3m-3 0h-3m-2-5a4 4 0 11-8 0 4 4 0 018 0zM3 20a6 6 0 0112 0v1H3v-1z"
              ></path>
            </svg>
          </span>
          <section
            id="headerSearch"
            class="text-xs bg-gray-600 rounded-lg p-0.5 flex items-center mr-2"
          >
            <input
              type="text"
              placeholder="Search"
              class="p-1 bg-gray-600 focus:outline-none"
            />
            <span class="px-1">
              <svg
                class="w-4 h-4"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                ></path>
              </svg>
            </span>
          </section>
          <span>
            <svg
              class="w-6 h-6"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"
              ></path>
            </svg>
          </span>
          <span>
            <svg
              class="w-6 h-6"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-8-3a1 1 0 00-.867.5 1 1 0 11-1.731-1A3 3 0 0113 8a3.001 3.001 0 01-2 2.83V11a1 1 0 11-2 0v-1a1 1 0 011-1 1 1 0 100-2zm0 8a1 1 0 100-2 1 1 0 000 2z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </span>
        </section>
      </header>
      <section
        id="call"
        class="flex justify-center items-center bg-gray-700 py-10"
      >
        <div id="callChildWrapper" class="space-y-2">
          <div id="callers" class="flex justify-center items-center space-x-4">
            <figure v-for="person in dms.slice(0, 2)" :key="person.id" class="">
              <img
                class="w-24 bg-indigo-300 rounded-full border-4 border-gray-700 hover:border-green-500"
                :src="person.avatar"
                alt=""
              />
            </figure>
          </div>
          <div id="callActions" class="">
            <ul class="text-white flex justify-center items-center space-x-2">
              <li class="cursor-pointer relative">
                <div
                  class="w-ful h-full p-3 bg-gray-600 rounded-full hover:bg-gray-800"
                >
                  <svg
                    class="w-8 h-8"
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M2 6a2 2 0 012-2h6a2 2 0 012 2v8a2 2 0 01-2 2H4a2 2 0 01-2-2V6zM14.553 7.106A1 1 0 0014 8v4a1 1 0 00.553.894l2 1A1 1 0 0018 13V7a1 1 0 00-1.447-.894l-2 1z"
                    ></path>
                  </svg>
                </div>
                <span
                  class="absolute bg-gray-700 rounded-full p-0.5 -bottom-1 -right-1"
                >
                  <svg
                    class="w-5 h-5 p-1 bg-gray-600 rounded-full hover:bg-gray-800"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M19 9l-7 7-7-7"
                    ></path>
                  </svg>
                </span>
              </li>
              <li
                class="p-3 bg-gray-600 rounded-full hover:bg-gray-800 cursor-pointer"
              >
                <svg
                  class="w-8 h-8"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M3 5a2 2 0 012-2h10a2 2 0 012 2v8a2 2 0 01-2 2h-2.22l.123.489.804.804A1 1 0 0113 18H7a1 1 0 01-.707-1.707l.804-.804L7.22 15H5a2 2 0 01-2-2V5zm5.771 7H5V5h10v7H8.771z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
              </li>
              <li
                class="p-3 bg-gray-600 rounded-full relative hover:bg-gray-800 cursor-pointer"
              >
                <svg
                  class="w-8 h-8"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M7 4a3 3 0 016 0v4a3 3 0 11-6 0V4zm4 10.93A7.001 7.001 0 0017 8a1 1 0 10-2 0A5 5 0 015 8a1 1 0 00-2 0 7.001 7.001 0 006 6.93V17H6a1 1 0 100 2h8a1 1 0 100-2h-3v-2.07z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
                <span
                  class="absolute bg-gray-700 rounded-full p-0.5 -bottom-1 -right-1"
                >
                  <svg
                    class="w-5 h-5 p-1 bg-gray-600 rounded-full"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M19 9l-7 7-7-7"
                    ></path>
                  </svg>
                </span>
              </li>
              <li class="p-3 bg-red-500 rounded-full cursor-pointer">
                <svg
                  class="w-8 h-8"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M2 3a1 1 0 011-1h2.153a1 1 0 01.986.836l.74 4.435a1 1 0 01-.54 1.06l-1.548.773a11.037 11.037 0 006.105 6.105l.774-1.548a1 1 0 011.059-.54l4.435.74a1 1 0 01.836.986V17a1 1 0 01-1 1h-2C7.82 18 2 12.18 2 5V3z"
                  ></path>
                  <path
                    d="M16.707 3.293a1 1 0 010 1.414L15.414 6l1.293 1.293a1 1 0 01-1.414 1.414L14 7.414l-1.293 1.293a1 1 0 11-1.414-1.414L12.586 6l-1.293-1.293a1 1 0 011.414-1.414L14 4.586l1.293-1.293a1 1 0 011.414 0z"
                  ></path>
                </svg>
              </li>
            </ul>
          </div>
        </div>
      </section>
      <section id="messages" class="flex-grow">h</section>
      <section id="typeMsg" class="p-3 text-gray-100">
        <div
          class="bg-gray-500 p-3 rounded-lg flex flex-start items-center space-x-2"
        >
          <figure class="text-gray-200">
            <svg
              class="w-6 h-6"
              fill="currentColor"
              viewBox="0 0 20 20"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </figure>
          <input
            class="flex-grow bg-gray-500 focus:outline-none"
            type="text"
            placeholder="Message @to"
          />
          <div id="typeIcons" class="flex justify-end items-center space-x-2">
            <figure class="">
              <svg
                class="w-6 h-6"
                fill="currentColor"
                viewBox="0 0 20 20"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  fill-rule="evenodd"
                  d="M5 5a3 3 0 015-2.236A3 3 0 0114.83 6H16a2 2 0 110 4h-5V9a1 1 0 10-2 0v1H4a2 2 0 110-4h1.17C5.06 5.687 5 5.35 5 5zm4 1V5a1 1 0 10-1 1h1zm3 0a1 1 0 10-1-1v1h1z"
                  clip-rule="evenodd"
                ></path>
                <path
                  d="M9 11H3v5a2 2 0 002 2h4v-7zM11 18h4a2 2 0 002-2v-5h-6v7z"
                ></path>
              </svg>
            </figure>
            <p
              class="bg-gray-100 px-0.5 py-1 text-gray-500 text-xs rounded-sm font-mono font-semibold"
            >
              GIF
            </p>
            <span
              class="filter-grayscale"
              @mouseover="
                currentEmoji = Math.floor(Math.random() * emojis.length)
              "
            >
              {{ emojis[currentEmoji] }}
            </span>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      servers: [
        {
          name: "Hanh Ngo",
          icon: "url",
        },
        {
          name: "Günhan Selaş",
          icon: "url",
        },
        {
          name: "Tailwincss",
          icon: "url",
        },
        {
          name: "Fularsız",
          icon: "url",
        },
        {
          name: "Masaüst",
          icon: "url",
        },
      ],
      currentEmoji: 0,
      emojis: [
        "😃",
        "😆",
        "😍",
        "😙",
        "😋",
        "🤗",
        "🤯",
        "🥳",
        "🤩",
        "👾",
        "🤖",
        "🤑",
      ],
      dms: [
        {
          id: 1,
          name: "Della McMenamie",
          email: "dmcmenamie0@clickbank.net",
          gender: "Genderfluid",
          ip_address: "248.75.194.217",
          avatar: "https://robohash.org/ideaqueiusto.png?size=96x96&set=set2",
        },
        {
          id: 2,
          name: "Orsa Heed",
          email: "oheed1@dagondesign.com",
          gender: "Genderqueer",
          ip_address: "79.23.24.150",
          avatar: "https://robohash.org/etametid.png?size=96x96&set=set4",
        },
        {
          id: 3,
          name: "Clem Yakunikov",
          email: "cyakunikov2@multiply.com",
          gender: "Female",
          ip_address: "188.211.62.26",
          avatar: "https://robohash.org/eafaciliseos.png?size=96x96&set=set1",
        },
        {
          id: 4,
          name: "Earvin Jopke",
          email: "ejopke3@cocolog-nifty.com",
          gender: "Female",
          ip_address: "43.94.153.242",
          avatar: "https://robohash.org/rerumsitillo.png?size=96x96&set=set1",
        },
        {
          id: 5,
          name: "Kaiser Baughn",
          email: "kbaughn4@forbes.com",
          gender: "Male",
          ip_address: "162.84.182.13",
          avatar:
            "https://robohash.org/nisianimidistinctio.png?size=96x96&set=set1",
        },
        {
          id: 6,
          name: "Tate Bazelle",
          email: "tbazelle5@yahoo.com",
          gender: "Genderfluid",
          ip_address: "217.144.5.121",
          avatar:
            "https://robohash.org/providentipsamquo.png?size=96x96&set=set1",
        },
        {
          id: 7,
          name: "Darby Seatter",
          email: "dseatter6@arstechnica.com",
          gender: "Polygender",
          ip_address: "221.71.216.248",
          avatar: "https://robohash.org/estettotam.png?size=96x96&set=set1",
        },
        {
          id: 8,
          name: "Marrilee Withrington",
          email: "mwithrington7@goodreads.com",
          gender: "Female",
          ip_address: "58.222.186.37",
          avatar: "https://robohash.org/utametearum.png?size=96x96&set=set1",
        },
        {
          id: 9,
          name: "Suellen Tonks",
          email: "stonks8@google.de",
          gender: "Male",
          ip_address: "178.84.78.103",
          avatar: "https://robohash.org/sitmaximedicta.png?size=96x96&set=set1",
        },
        {
          id: 10,
          name: "Bronnie Wendover",
          email: "bwendover9@aol.com",
          gender: "Male",
          ip_address: "3.152.108.239",
          avatar: "https://robohash.org/etadodio.png?size=96x96&set=set1",
        },
        {
          id: 11,
          name: "Suellen Tonks",
          email: "stonks8@google.de",
          gender: "Male",
          ip_address: "178.84.78.103",
          avatar: "https://robohash.org/sitmaximedicta.png?size=96x96&set=set1",
        },
        {
          id: 12,
          name: "Bronnie Wendover",
          email: "bwendover9@aol.com",
          gender: "Male",
          ip_address: "3.152.108.239",
          avatar: "https://robohash.org/etadodio.png?size=96x96&set=set1",
        },
        {
          id: 11,
          name: "Suellen Tonks",
          email: "stonks8@google.de",
          gender: "Male",
          ip_address: "178.84.78.103",
          avatar: "https://robohash.org/sitmaximedicta.png?size=96x96&set=set1",
        },
        {
          id: 12,
          name: "Bronnie Wendover",
          email: "bwendover9@aol.com",
          gender: "Male",
          ip_address: "3.152.108.239",
          avatar: "https://robohash.org/etadodio.png?size=96x96&set=set1",
        },
        {
          id: 13,
          name: "Suellen Tonks",
          email: "stonks8@google.de",
          gender: "Male",
          ip_address: "178.84.78.103",
          avatar: "https://robohash.org/sitmaximedicta.png?size=96x96&set=set1",
        },
        {
          id: 14,
          name: "Bronnie Wendover",
          email: "bwendover9@aol.com",
          gender: "Male",
          ip_address: "3.152.108.239",
          avatar: "https://robohash.org/etadodio.png?size=96x96&set=set1",
        },
        {
          id: 15,
          name: "Suellen Tonks",
          email: "stonks8@google.de",
          gender: "Male",
          ip_address: "178.84.78.103",
          avatar: "https://robohash.org/sitmaximedicta.png?size=96x96&set=set1",
        },
        {
          id: 16,
          name: "Bronnie Wendover",
          email: "bwendover9@aol.com",
          gender: "Male",
          ip_address: "3.152.108.239",
          avatar: "https://robohash.org/etadodio.png?size=96x96&set=set1",
        },
      ],
    };
  },
  methods: {
    initials(string) {
      let array = string.split(" ");
      return array.map((item) => item[0]).join("");
    },
    deleteDm(id) {
      let ourItem = this.dms.find((dm) => dm.id === id);
      ourItem.isDeleted = true;
      if (ourItem)
        this.$set(
          this.dms,
          this.dms.findIndex((dm) => dm.id === id),
          ourItem
        );
    },
  },
  computed: {
    notDeletedDms() {
      return this.dms.filter((dm) => dm.isDeleted !== true);
    },
  },
};
</script>

<style scoped>
.friends-icon::before,
.nitro-icon::before {
  content: url('data:image/svg+xml;utf8,<svg fill="none" stroke="gray" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>');
  color: #000;
  display: inline-block;
  width: 1.4rem;
  padding-right: 2px;
}

.atIcon::before {
  content: url('data:image/svg+xml;utf8, <svg  fill="none" stroke="transparen" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"></path></svg>');
  clip-path: url('data:image/svg+xml;utf8, <svg class="w-36" fill="none" stroke="black" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 12a4 4 0 10-8 0 4 4 0 008 0zm0 0v1.5a2.5 2.5 0 005 0V12a9 9 0 10-9 9m4.5-1.206a8.959 8.959 0 01-4.5 1.207"></path></svg>');
  width: 1.4rem;
  display: inline-block;
}
.appearOnHover {
  visibility: hidden;
}
.list:hover .appearOnHover {
  visibility: visible;
}
.tool-button {
  position: relative;
}
.tool-button:hover .tool-text,
.tool-button:hover .tool-text-copy {
  visibility: visible;
  opacity: 1;
  transition: opacity 0.2s;
}
.tool-text,
.tool-text-copy {
  position: absolute;
  z-index: 1;
  bottom: 100%;
  right: 50%;
  margin-right: -1.75rem;
  visibility: hidden;
  opacity: 0;
}
.tool-text::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #111827 transparent transparent transparent;
}
.tool-text-copy::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #34D399 transparent transparent transparent;
}

::-webkit-scrollbar {
  width: 0.4rem;
}

::-webkit-scrollbar-track {
  background: #1F2937;
}

::-webkit-scrollbar-thumb {
  visibility: hidden;
  background: #4B5563;
}

.link-list:hover::-webkit-scrollbar-thumb {
  cursor: pointer;
  visibility: visible;
}

.filter-grayscale {
  filter: grayscale(100%);
  transition: transform 0.2s ease;
  transform: scale(1);
}
.filter-grayscale:hover {
  filter: grayscale(0%);
  transform: scale(1.2);
  transform-origin: center;
}

*[data-tooltip] {
  position: relative;
}

*[data-tooltip]::before {
  content: attr(data-tooltip);
  white-space: nowrap;
  width: max-content;
  position: absolute;
  bottom: 0;
  left: 0;
  padding: 0.5rem;
  font-size: 0.8em;
  font-weight: 500;
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 0.5rem;
  transform: scale(0);
}

*[data-tooltip]:hover::before {
  bottom: 115%;
  right: 50%;
  transform: scale(1);
}

*[data-tooltip]:hover::after {
  content: "";
  width: 0;
  height: 0;
  position: absolute;
  top: -15%;
  left: 25%;
  border: 0.3rem solid transparent;
  border-top: 0.3rem solid rgba(0, 0, 0, 0.7);
}

.pseudo-bg-green:hover::before {
  background-color: rgba(0, 197, 110, 0.8);
}
.pseudo-bg-green:hover::after {
  border: 0.3rem solid transparent;
  border-top: 0.3rem solid rgba(0, 197, 110, 0.7);
}
</style>

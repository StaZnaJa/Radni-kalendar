// ================================
// Radni kalendar – SERVICE WORKER
// ================================

// 🔴 SVAKA IZMJENA KODA = PROMENA VERZIJE
const CACHE_NAME = 'pio-kalkulator-cache-v1000';

// 🔴 TAČNE PUTANJE ZA GITHUB PAGES
const FILES_TO_CACHE = [
  '/Radni-kalendar/',
  '/Radni-kalendar/index.html',
  '/Radni-kalendar/manifest.json',
  '/Radni-kalendar/icon-192.png',
  '/Radni-kalendar/icon-512.png'
];

// ================================
// INSTALL – keširanje + instant aktivacija
// ================================
self.addEventListener('install', event => {
  self.skipWaiting();

  event.waitUntil(
    caches.open(CACHE_NAME).then(cache => {
      return cache.addAll(FILES_TO_CACHE);
    })
  );
});

// ================================
// ACTIVATE – briše SVE stare keševe
// ================================
self.addEventListener('activate', event => {
  event.waitUntil(
    caches.keys().then(keys =>
      Promise.all(
        keys.map(key => {
          if (key !== CACHE_NAME) {
            return caches.delete(key);
          }
        })
      )
    )
  );

  self.clients.claim();
});

// ================================
// FETCH – network-first (uvek novi kod)
// ================================
self.addEventListener('fetch', event => {
  event.respondWith(
    fetch(event.request)
      .then(response => response)
      .catch(() => caches.match(event.request))
  );
});

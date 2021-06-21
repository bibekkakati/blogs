## Introducing SURL 🎊 Shorten your URL

We all are aware of different URL shortening services like bit.ly, TinyURL etc. I was thinking of building a similar application as it seems very simple but it is very challenging when you consider scalability and reliability. Finally, I got the opportunity to build the application because of [#harperdbhackathon](https://hashnode.com/n/harperdbhackathon) and it is here.

### Introducing SURL 🎊

![s1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624213602609/MfpUrq6Tt.png)

You can try it out here: [surl.bibekkakati.me](https://surl.bibekkakati.me/h0Q0000)

---

```yaml
- What is SURL
- Why I created SURL
- How to use
- Current Features
- System Overview
- Project Code
- Tech Stack
- Upcoming Features
- Challenges
- Live Demo
```
---

### What is SURL? 🔗

It is a web-based URL shortening service where user can generate a shorter form of their long URL.

### Why I created SURL? ✨

The reason behind creating this service is that I have always been fascinated with the working, implementation and management of this kind of services because of its backend engineering, system design, scalability related complexities.

![s2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624212651248/aEkphoBtM.png)

### How to use? 📙

- Go to [surl.bibekkakati.me](https://surl.bibekkakati.me/h0Q0000)

- Paste your long URL

- Once a short URL is generated, it will be shown on the screen

- Click it to copy to clipboard

![ss3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624218406936/TAOe7qwkv.png)

### Current Features 💡

- Generate a short URL instantly.

- Most important feature 😉 `dark` and `light` mode.

- Check the total URL hits by going to the `/hits` path of your short URL.

> If your short URL is `https://surl.bibekkakati.me/h0QuiOk`, then go to `https://surl.bibekkakati.me/h0QuiOk/hits`.

### System Overview 👀

Two services are there:

- `SURL service` is the main client-facing service, which is responsible for serving static files and issuing a short URL against a provided long URL by the user with the help of an API. The service is built by keeping scalability in mind so we can deploy multiple instances of this service without any issue to balance the incoming request load.

- `KeyGen service`  is a standalone service that is responsible for generating unique keys for all the active `SURL service`. It generates 100,000 unique keys on request from any `SURL service` and returns the keys in response. Both the service communicate using gRPC.

> Caching is used for faster access and to reduce the load on the database.

### Project Code 👨‍💻

- SURL service: https://github.com/bibekkakati/surl

- KeyGen service: https://github.com/bibekkakati/surl-key-generator

### Tech Stack 💻

- Node.js (Express.js) - Backend framework

- HarperDB - Database

- Nginx - Proxy Server

- Azure Cloud - Deployment

### Upcoming Features 🔮

- User authentication

- Dashboard

- Custom short URL.

- Analytics like unique visits, visitor's country, city etc.

- QR-Code for short URL

- Private URL i.e, a visitor needs permission to access it or an access code.

### Challenges

- Building a reliable and fast system.

- Tuning the server to handle larger concurrent users. Still trying to get a better result.

- Generating unique keys (short URL), which I achieved with the counter based approach.

> KeyGen service assures that the same key will not be generated more than once.

### Live Demo 👇

[https://surl.bibekkakati.me](https://surl.bibekkakati.me/h0Q0000)

---

Thank you for reading 🙏

If you enjoyed this article or found it helpful, give it a thumbs-up 👍

Feel free to connect 👋

[Twitter](https://twitter.com/kakatibibek) | [Instagram](https://instagram.com/bibekkakati) | [LinkedIn](https://linkedin.com/in/bibekkakati)


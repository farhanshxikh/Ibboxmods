Timer timer = new Timer();
// 1-Minute Period and Timer
timer.scheduleAtFixedRate(new TimerTask() {
    @Override
    public void run() {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Calendar calendar = Calendar.getInstance(TimeZone.getTimeZone("UTC"));
                
                int seconds = calendar.get(Calendar.SECOND);
                int remainingSeconds = 60 - seconds;
                int minutes = calendar.get(Calendar.MINUTE);
                int totalMinutes = calendar.get(Calendar.HOUR_OF_DAY) * 60 + minutes;

                // Format the period number and update the UI
                String period = new SimpleDateFormat("yyyyMMdd").format(calendar.getTime())
                        + "1000" + (10001 + totalMinutes);
                period1m.setText(period);

                // Format the timer time as " XX : XX"
                String formattedTime = String.format("   %02d  :  %02d", 0, remainingSeconds);
                timer1m.setText(formattedTime);
            }
        });
    }
}, 0, 1000);  // Update every second

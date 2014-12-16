blog
====


        SimpleDateFormat timeZoneFormatter = new SimpleDateFormat(format);
        if (StringUtils.isNotBlank(timezone)) {
            timeZoneFormatter.setTimeZone(TimeZone.getTimeZone(timezone));
        }

        Date parsedDate = SIMPLE_UTC_DATE_FORMATTER.parse(utcDate);
        String convertedDate = timeZoneFormatter.format(parsedDate);
        return convertedDate;

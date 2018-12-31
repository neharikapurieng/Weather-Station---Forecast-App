# Weather-Station---Forecast-App

/**
 * A weather forecast app determines if the pressure readings from its
 * subscribed weather station, if any, indicate it is likely to rain due to a
 * reduction on the pressure level.
 */
public class ForecastApp extends WeatherObserver {

	/**
	 * Update the reading of this weather observer. Update the current and last
	 * readings of pressure.
	 */
	private WeatherStation wSta;
	private double prSig, lastPrSig;

	public void update() {
		
		if (this.prSig != 0) {
			this.lastPrSig = this.prSig;
		} else {
			this.lastPrSig = wSta.getPressure();
		}
		this.prSig = wSta.getPressure();
	}

	/* See the method description in the parent class */
	public WeatherStation getWeatherStation() {
		
		return wSta;
	}

	/* See the method description in the parent class */
	public void setWeatherStation(WeatherStation ws) {
		
		this.wSta = ws;
	}

	/**
	 * Get the pressure level read from the last update.
	 * 
	 * @return pressure level read from the last update
	 */
	public double getCurrentPressure() {
		
		return this.prSig;
	}

	/**
	 * Get the pressure level read from the second last update.
	 * 
	 * @return pressure level read from the second last update
	 */
	public double getLastPressure() {
		
		return this.lastPrSig;
	}

	/**
	 * Based on the last and second last readings of the pressure level, it is
	 * determined as likely to rain if there is a reduction on the pressure level;
	 * otherwise it is unlikely to rain.
	 * 
	 * @return whether or not it is likely to rain.
	 */
	public boolean isLikelyToRain() {
		
		if (this.prSig < this.lastPrSig) {
			return true;
		} else {
			return false;
		}
	}
}

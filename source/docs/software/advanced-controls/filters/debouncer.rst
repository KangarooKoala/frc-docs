# Debouncer

A debouncer is a filter used to eliminate unwanted quick on/off cycles (termed "bounces," originally from the physical vibrations of a switch as it is thrown). These cycles are usually due to a sensor error like noise or reflections and not the actual event the sensor is trying to record.

Debouncing is implemented in WPILib by the ``Debouncer`` class ([Java](https://github.wpilib.org/allwpilib/docs/release/java/edu/wpi/first/math/filter/Debouncer.html), [C++](https://github.wpilib.org/allwpilib/docs/release/cpp/classfrc_1_1_debouncer.html), :external:py:class:`Python <wpimath.filter.Debouncer>`), which filters a boolean stream so that the output only changes if the input sustains a change for some nominal time period.

## Modes

The WPILib ``Debouncer`` can be configured in three different modes:

* Rising (default): Debounces rising edges (transitions from `false` to `true`) only.
* Falling: Debounces falling edges (transitions from `true` to `false`) only.
* Both: Debounces all transitions.

## Usage

.. tab-set-code::

  ```java
  // Initializes a DigitalInput on DIO 0
  DigitalInput input = new DigitalInput(0);
  // Creates a Debouncer in "both" mode.
  Debouncer m_debouncer = new Debouncer(0.1, Debouncer.DebounceType.kBoth);
  // So if currently false the signal must go true for at least .1 seconds before being read as a True signal.
  if (m_debouncer.calculate(input.get())) {
    // Do something now that the DI is True.
  }
  ```

  ```c++
  // Initializes a DigitalInput on DIO 0
  frc::DigitalInput input{0};
  // Creates a Debouncer in "both" mode.
  frc::Debouncer m_debouncer{100_ms, frc::Debouncer::DebounceType::kBoth};
  // So if currently false the signal must go true for at least .1 seconds before being read as a True signal.
  if (m_debouncer.calculate(input.Get())) {
    // Do something now that the DI is True.
  }
  ```

  ```python
  from wpilib import DigitalInput
  from wpimath.filter import Debouncer
  # Initializes a DigitalInput on DIO 0
  self.input = DigitalInput(0)
  # Creates a Debouncer in "both" mode with a debounce time of 0.1 seconds
  self.debouncer = Debouncer(0.1, Debouncer.DebounceType.kBoth)
  # If currently false, the signal must go true for at least 0.1 seconds before being read as a True signal.
  if self.debouncer.calculate(self.input.get()):
      # Do something now that the DI is True.
      pass
  ```


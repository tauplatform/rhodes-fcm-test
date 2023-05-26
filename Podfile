platform :ios, '12.0'
use_frameworks!

pod 'Firebase/Auth'
pod 'Firebase/Firestore'
pod 'Firebase/Messaging'

target 'rhorunner' do
end

post_install do |installer|
    installer.pods_project.targets.each do |target|
        if target.name == "Pods-rhorunner"
            puts "Updating #{target.name} OTHER_LDFLAGS"
            target.build_configurations.each do |config|
                xcconfig_path = config.base_configuration_reference.real_path

                # read from xcconfig to build_settings dictionary
                build_settings = Hash[*File.read(xcconfig_path).lines.map{|x| x.split(/\s*=\s*/, 2)}.flatten]

                # modify OTHER_LDFLAGS
                config_line = build_settings['OTHER_LDFLAGS']
                if (config_line != nil)
                    config_line = config_line.gsub("$(inherited) ","")
                    build_settings['OTHER_LDFLAGS'] = config_line
                    puts "updated OTHER_LDFLAGS = "+config_line
                end

                # write build_settings dictionary to xcconfig
                File.open(xcconfig_path, "w") do |file|
                  build_settings.each do |key,value|
                    file.write(key + " = " + value)
                  end
                end
            end
        end
    end
end
